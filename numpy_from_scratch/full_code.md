# Full Code
Below is all the code that we have written to date.

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)

{% highlight python %}

import copy

def gen_mat(size, value=0):
    generated_mat = []
    for i in range(size[0]):
        generated_mat.append([value for j in range(size[1])])
    return Mat(generated_mat)

def eye(size):
    eye = gen_mat(size)
    for i in range(size[0]):
        eye.data[i][i] = 1
    return eye

def print_mat(self):
    for row in self.data:
        print(row)
    print()

class Mat:
    def __init__(self, data):
        self.data = data

    def transpose(self):
        transposed = []
        for row_idx, row in enumerate(self.data):
            for col_idx, col in enumerate(row):
                # first time through, make new row for each old column
                if row_idx == 0:
                    transposed.append([col])
                else:
                    # append to newly created rows
                    transposed[col_idx].append(col)
            self.data = transposed
        return self

    def scale(self, scalar):
        for row_idx, row in enumerate(self.data):
            for col_idx in range(len(row)):
                self.data[row_idx][col_idx] *= scalar
        return self

    def add(self, new_mat):
        added_rows = []
        for rows in zip(self.data, new_mat.data):
            added_cols = []
            for cols in zip(rows[0],rows[1]):
                added_cols.append(sum(list(cols)))
            added_rows.append(added_cols)
        self.data = added_rows
        return self

    def subtract(self, new_mat):
        # reverse sign of second matrix
        new_mat.scale(-1)
        # use add function
        return self.add(new_mat)

    def dot(self, new_mat):
        # make both vectors rows with transpose
        if len(self.data) != 1:
            self.transpose()
        if len(new_mat.data) != 1:
            new_mat.transpose()
        # compute dot product
        dot_prod = []
        for cols in zip(self.data[0], new_mat.data[0]):
            dot_prod.append(cols[0]*cols[1])
        dot_prod = sum(dot_prod)
        return dot_prod

    def multiply(self, new_mat):
        # preallocate empty matrix
        multiplied = gen_mat([len(self.data), len(new_mat.data[0])])
        # transpose one matrix, take a bunch of dot products
        transposed = new_mat.transpose()
        for row_idx, row in enumerate(self.data):
            tmp_row = Mat([row])
            for col_idx, col in enumerate(transposed.data):
                tmp_col = Mat([col])
                tmp_dot = tmp_row.dot(tmp_col)
                # enter the dot product into our final matrix
                multiplied.data[row_idx][col_idx] = tmp_dot
        return multiplied

    def diag(self):
        diag_vals = []
        for i in range(min(len(self.data), len(self.data[0]))):
            diag_vals.append(self.data[i][i])
        return diag_vals

    def elimination(self):
        # should do some row exchanges for numerical stability...

        # we assume the matrix is invertible
        singular = 0

        # create identity matrix which we'll turn into an E matrix
        tmpE = gen_mat([len(self.data),len(self.data[0])])
        for row_idx in range(len(tmpE.data)):
            tmpE.data[row_idx][row_idx] = 1

        # create a permutation matrix for row exchanges
        P = gen_mat([len(self.data),len(self.data)])
        for row_idx in range(len(tmpE.data)):
            P.data[row_idx][row_idx] = 1

        currentE = copy.deepcopy(tmpE)
        U = copy.deepcopy(self)
        pivot_count = 0
        row_exchange_count = 0
        for row_idx in range(len(U.data)-1):
            for sub_row in range(row_idx+1, len(U.data)):
                # create elimination mat
                nextE = copy.deepcopy(tmpE)

                # handle a zero in the pivot position
                if U.data[row_idx][pivot_count] == 0:
                    row_exchange_count += 1
                    # look for a non-zero value to use as the pivot
                    options = [row[pivot_count] for row in U.data[sub_row:]]
                    exchange = sub_row + options.index(max(options, key=abs))

                    # build and apply a purmutation matrix
                    P = copy.deepcopy(P)
                    P.data[row_idx][pivot_count] = 0
                    P.data[row_idx][exchange] = 1
                    P.data[exchange][exchange] = 0
                    P.data[exchange][pivot_count] = 1
                    U = P.multiply(U)

                # get copies of the rows
                row_above = copy.deepcopy(Mat([U.data[row_idx]]))
                row_below = copy.deepcopy(Mat([U.data[sub_row]]))

                # check if the permutation avoided a zero in the pivot position
                if U.data[sub_row][sub_row] == 0:
                    singular = 1
                    return currentE, self, U, singular, row_exchange_count

                # determine how much to subtract to create a zero
                ratio = row_below.data[0][pivot_count]/row_above.data[0][pivot_count]
                # do the subtraction
                row_above.scale(ratio)
                row_below = row_below.subtract(row_above)
                # add to our E
                nextE.data[sub_row][row_idx] = -ratio
                # add to our U
                U.data[sub_row] = row_below.data[0]
                # update the overall E
                currentE = nextE.multiply(currentE)
            pivot_count += 1
        return currentE, self, U, singular, row_exchange_count

    def pivots(self):
        # find U
        _, _, U, _, _ = self.elimination()
        # extract the non-zeros on the diagonal
        diag_vals = U.diag()
        pivot_info = [(i, val) for i, val in enumerate(diag_vals) if val]
        return pivot_info

    def rank(self):
        pivot_info = self.pivots()
        return len(pivot_info)

    def is_singular(self):
        _, _, _, singular, _ = self.elimination()
        return singular

    def determinant(self):
        # find U
        _, _, U, _, row_exchange_count = self.elimination()
        # muliply the pivots
        det = 1
        diag_vals = U.diag()
        for val in diag_vals:
            det *= val
        # if an odd number of row exchanges, multiply determinant by minus one
        if row_exchange_count % 2:
            det *= -1
        return det

    def inverse(self):
        size = [len(self.data), len(self.data[0])]

        # create [A I]
        I = eye(size)
        augmented = Mat([rows[0]+rows[1]  for rows in zip(self.data, I.data)])

        # perform elimination to get to [U ~inv]
        _, _, U, singular, _ = augmented.elimination()

        if singular:
            print('Matrix is singular!')
            return None

        # seperate augmented into U and ~inv
        tmp_fU = Mat([Urow[0:size[1]] for Urow in U.data])
        tmp_inv = Mat([Urow[size[1]:] for Urow in U.data])

        # creae anti-diag I
        antiI = gen_mat(size)
        for i, j in enumerate(reversed(range(size[1]))):
            antiI.data[i][j] = 1

        # multiply U and ~inv on both sides by anti-diag I
        fU = antiI.multiply(tmp_fU)
        fU = fU.multiply(antiI)
        f_tmp_inv = antiI.multiply(tmp_inv)
        f_tmp_inv.multiply(antiI)

        # put fU back into [fU  f~inv]
        augmented = Mat([rows[0]+rows[1] for rows in zip(fU.data, f_tmp_inv.data)])

        # perform elimination again to get to [cI cA^-1]
        _, _, U, singular, _ = augmented.elimination()

        # divide each row by c to get [I A^-1]
        div = gen_mat(size)
        for i in range(size[0]):
            div.data[i][i] = 1/U.data[i][i]
        inv = div.multiply(U)

        # flip back
        inv = antiI.multiply(inv)
        for i in range(size[1]):
            inv.data[i] = inv.data[i][size[1]:]
        return inv

{% endhighlight %}

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)

