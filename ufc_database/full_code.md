# Full Code
Below is all the code that we have written to date.

[back to project main page](./ufc_database.md)\
[back to home](../index.md)

{% highlight python %}

from bs4 import BeautifulSoup as bs
import requests
import re
import pandas as pd
import wikipedia as wp
from prettytable import PrettyTable
import random

# initialise a table object with column names
t = PrettyTable(['Event', 'Weight', 'Fighter1', 'Fighter2'])
t.align='l'
t.border=False

# grab all the links on the List_of_UFC_events wiki page
res = requests.get("https://en.wikipedia.org/wiki/List_of_UFC_events")
soup = bs(res.text, "html.parser")

# latest event already in the database
latest = 255
future = 259

# avoid visiting the same page more that once
tried = []
with open("/home/mattb/videos/ufc/ufc_database.txt", "a") as f:
    for link in soup.find_all("a"):
        try:
            url = link.get("href", "")

            # if the link looks like a ufc event that we've not tried yet
            if bool(re.search('UFC_\d+$', url)) and (url not in tried):
                tried.append(url)
                event = int(re.findall('\d+$', url)[0])
                if event > latest and event < future:

                    print(url)

                    # read the page
                    html = wp.page(url[6:], auto_suggest=False).html().encode("UTF-8")
                    # pull 3rd table
                    df = pd.read_html(html)[2]

                    # put the zero padded ufc number as the Event column
                    df.insert(0, "Event", ('UFC_' + url[10:].zfill(4)))
                    # get rid of columns I don't want (brittle approach...)
                    df = df.drop(df.columns[[3,5,6,7,8]], axis=1)
                    # change df from a multiindex to single indexed object
                    df.columns = df.columns.get_level_values(0)
                    # rename the colums sensibly
                    df.columns = ['Event', 'Weight', 'Fighter1', 'Fighter2']
                    # find where the prelims start
                    index = df[df['Weight'].str.contains('Preliminary')].index[0].item()
                    # select only the main card
                    df = df[:index]
                    # strip the indices and column names and convert to csv string
                    data = df.to_csv(index=False, header=False)
                    # each line is a list item contatining a csv string
                    data = data.splitlines()
                    # shuffle order of fighters (the winner is always listed first)
                    for line in data:
                        entries = line.split(',')
                        copy = entries[2:]
                        random.shuffle(copy)
                        entries[2:] = copy
                        # add each csv to a column which is nicely aligned
                        t.add_row(entries)

        # just move on from any errors
        except:
            print('error')
        pass

    # if we're just adding to an existing database, the header already exists
    if latest > 0:
        t.header = False

    # sort into chronological order and save
    f.write(str(t.get_string(sortby=('Event'))))
    f.write('\n')

{% endhighlight %}

[back to project main page](./ufc_database.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/ufc_database/full_code.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

