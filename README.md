# pitchfork-analysis
Doing some EDA on pitchforks reviews of the last ~20 years.

We have used this dataset on kaggle https://www.kaggle.com/nolanbconaway/pitchfork-data, which provides us with info of over 18000 pitchfork reviews.
Some of the tables had to be changed for better useability.

We then scraped wikipedia to look for the genders of all the artists in the list. The dataset contains 8715 individual artists. 
Our methods allowed for immediate recognition of approximately 2200 artists' genders.

This is one of three methods, that we have tried.

1. The first one was inspired by this repo https://github.com/rkibria/rkibria.github.com/blob/master/scrape_wiki_categories.md. Wikipedia categorizes every article. Some of these articles could be for example "Female Rapper", "Male African American Musician", ....
We can then search through these categories to look for keywords such as "female", "Female", "transgender", ...
This method certainly works to some extent, but comparing to the method we ended up using it yielded worse results. On a random subset of 200 examples, this method only gave me 3 genders, that the other method didn't find whereas the other one found 12 genders this one didn't find. Nonetheless it might be worth running this method at some point overnight and merging the results in the end

2. Another method would be to look through the first (1 to n) paragraphs of each article and count the occurences of "he" vs "she" and define the gender by whichever pronoun has been used more. This method is of course very prone to error and upon inspecting a few examples it doesn't seem like the right way to go (Although it has indeed found a few genders where the other methods didn't get any result). 

3. Most Wikipedia pages have an associated Wikidata page, where we can find a lot of info about the associated artist, gender being one of them. This is the most reliable method and is the one we used to get most of the genders. We then filled up some "unknown" ones with the genders we got from the category-approach. The second method should probably not be used as it results in too many errors.

All methods have problems with bands / doubleacts. However, 1/4 of all the data should already be enough to get statistically relevant information. One could of course look through bandmembers and individually repeat the above steps to create a more complete image of bands' genders but due to the lack of many bandmembers' wikipedia pages we will not do this here.
