# pitchfork-analysis
Doing some EDA on pitchforks reviews of the last ~20 years.

## questions:

1. Have reviews gotten better or worse over the years.
2. How big is the nostalgia factor - Do albums from the past (pre 1999) receive generally better reviews than contemporary albums
3. What genres are more likely to do well
4. Does gender play a role in the rating score and how has the musical landscape changed in regards to gender representation in the past 2 decades

## methods
Using bs4 I scraped all of the reviews from the pitchfork website up to August 19th 2020.

I then scraped wikipedia to look for the genders of all the artists in the list. The dataset contains 10620 individual artists. 
My methods allowed for immediate recognition of 2919 artists' genders. While this is less than one third of the whole list, keep in mind that a lot of the artists are bands and can as such not necessarily fit a category. Furthermore one third of all entries should be enough to claim statistical significance. More on this later...

Later I used pandas / sqlite3 / matplotlib / ... to create the dataframes and perform the EDA.

### wikipedia scraping - 3 methods

1. The first method was inspired by this repo https://github.com/rkibria/rkibria.github.com/blob/master/scrape_wiki_categories.md. Wikipedia categorizes every article. Some of these articles could be for example "Female Rapper", "Male African American Musician", ....
We can then search through these categories to look for keywords such as "female", "Female", "transgender", ...
This method certainly works to some extent, but comparing to the main method we ended up using it yielded worse results. On a random subset of 200 examples, this method only gave me 3 genders, that the other method didn't find whereas the other one found 12 genders this one didn't find.

2. Another method would be to look through the first (1 to n) paragraphs of each article and count the occurences of "he" vs "she" and define the gender by whichever pronoun has been used more. This method is of course very prone to error and upon inspecting a few examples it doesn't seem like the right way to go (Although it has indeed found a few genders where the other methods didn't get any result). 

3. Most Wikipedia pages have an associated Wikidata page, where we can find a lot of info about the associated artist, gender being one of them. This is the most reliable method and is the one we used to get most of the genders. We then filled up some "unknown" ones with the genders we got from the category-approach. The second method should probably not be used as it results in too many errors.

All methods have problems with bands / doubleacts.. One could of course look through bandmembers and individually repeat the above steps to create a more complete image of bands' genders but due to the lack of many bandmembers' wikipedia pages I will not be doing this here.
