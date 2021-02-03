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
        multiplied = []
        # transpose one matrix, take a bunch of dot products
        transposed = new_mat.transpose()
        for row_idx, row in enumerate(self.data):
            tmp_row = Mat([row])
            for col_idx, col in enumerate(transposed.data):
                tmp_col = Mat([col])
                tmp_dot = tmp_row.dot(tmp_col)

                # first time through, make new row for each old column
                if row_idx == 0:
                    multiplied.append([tmp_dot])
                else:
                    # append to newly created rows
                    multiplied[col_idx].append(tmp_dot)
        return Mat(multiplied).transpose()

    def elimination(self):
        # need to handle cases where a zero is already below the pivot
        # should do some row exchanges for numerical stability...

        # create identity matrix which we'll turn into an E matrix
        tmpE = gen_mat([len(self.data),len(self.data[0])])
        for row_idx in range(len(tmpE.data)):
            tmpE.data[row_idx][row_idx] = 1

        currentE = copy.deepcopy(tmpE)
        U = copy.deepcopy(self)
        pivot_count = 0
        for row_idx in range(len(U.data)-1):
            for sub_row in range(row_idx+1, len(U.data)):
                # create elimination mat
                nextE = copy.deepcopy(tmpE)
                # get copies of the rows
                row_above = copy.deepcopy(Mat([U.data[row_idx]]))
                row_below = copy.deepcopy(Mat([U.data[sub_row]]))
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
        return currentE, self, U

{% endhighlight %}

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
