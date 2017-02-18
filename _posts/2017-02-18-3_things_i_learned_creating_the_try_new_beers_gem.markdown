---
layout: post
title:  "  3 Things I Learned Creating The Try New Beers Gem"
date:   2017-02-18 16:45:51 -0500
---


Hey there... I didn't hear you come in, but stay a while (or at least until the end of this blog post). I'm going to share with you 5 Things I learned while working on the Gem project. 


**1. Zip Method**

This may be my new favorite method when it comes dealing with multiple arrays. Essentially the Gem I created shows a user the top 250 beers, the user can then choose a beer based on number, and then it takes them right to profile page of that beer.

I created a BeerReview object that has 5 attributes: name, brewery, type, rating, profile. I used Nokogiri to scrape the site based on attributes. For example:

```
def self.breweries
   ` @breweries ||= @doc.search("div#extendedInfo a").children.select.each_with_index { |children, i| i.even? }.collect {|e|  e.text}`
end
```

Returned all the breweries of all beers in an array. I did the same for the other 4 attributes. As you can imagine, now I have 5 elements in 5 different arrays to make one BeerReview. I have to somehow squish together 5 arrays to get a single BeerReview. Yikes! I know, but have no fear the Zip Method is here. 

The really cool thing about the Zip method is that it merges corresponding elements from each array with one simple and easy to use method, and returns the corresponding elements in a single array. So here is a quick example:

```
names = ["Toppling Goliath", "Good Morning", "Pliny The Younger"]
breweries = ["Lagunitas", "Goose Island", "Brookly Brewery"]
types = ["IPA", "Imperial Stout", "American Double"]
ratings = ["4.5", "4.3", "3.37"]
profile = ["profile/23222/78820/", "profile/13371/", "profile/28743/87846/"] #we'll talk more on why these are important
```

I created a new array and used the zip method:

```
beer_review_array = names.zip(types, breweries, ratings, profiles)
```

Which gave me exactly what I wanted....a BeerReview.

```
beer_review_array = [["Toppling Goliath", "Lagunitas", "IPA", "4.5", "profile/23222/78820/"], ["Good Morning", "Goose Island", "Imperial Stout", "4.5",  "profile/13371/"], ["Pliny The Younger", "Brooklyn Brewery", "American Double", "3.37", "profile/28743/87846/"]]
```
The next time you find yourself needing to merge elements from different arrays, keep the Zip Method in mind.


**2. Navigating To A Webpage From Terminal**

Ok, so this was actually WAAAAAYYYY easier than I anticipated. In fact, it was so easy that I literally LOLd (is that a word?) after I wrote the code for it.

Remember the profile array above? So I need those in order to navigate to the corresponding profile of that beer so that users could learn more. So here is how I did it:

I set the profile attribute for every review

```
def self.scrape_all
    self.get_page
    beer_review_array = names.zip(types, breweries, ratings, profiles)
    (0..beer_review_array.size-1).to_a.each_with_index do |i|
    beer_review.name = beer_review_array[i][0]
    beer_review.type = beer_review_array[i][1]
    beer_review.brewery = beer_review_array[i][2]
    beer_review.rating = beer_review_array[i][3].to_f
    **beer_review.profile = beer_review_array[i][4]**
    beer_review.save
 end
```
    
In the CLI it returned the review with the profile URL. So this...
					
Kentucky Brunch Brand Stout, American Double / Imperial Stout, Toppling Goliath Brewing Company, 4.73,                           https://www.beeradvocate.com/beer/profile/23222/78820/

.... is equal to this.
							
	puts "#{i}. #{b.name}, #{b.type}, #{b.brewery}, #{b.rating}, https://www.beeradvocate.com#{b.profile}"

 
Simply use the open url with back ticks. Just like this

                  input = gets.strip.to_i
                  beer = BeerReview.find_by_index(input.to_i-1)
                  `open #{"https://www.beeradvocate.com#{beer.profile}"}`
                


 Once a user picks a beer, it navigates to the corresponding profile.






**3. Getting Creative With Your Scraping**

I had a really tought time extracting types and breweries, no matter how specific I got with my `.search`. It was either scraping neither or both. I'm not sure as to the exact reason why (please leave a comment if you know why :)  ), but as I examined the XML further I noticed that both were children of an object. One was even and the other was odd consistently. So in order to scrape it I had to do the following:
	
	
```
def self.types
    @types ||= @doc.search("div#extendedInfo a").children.select.each_with_index { |children, i| i.odd? }.collect {|e| e.text}
  end

  def self.breweries
    @breweries ||= @doc.search("div#extendedInfo a").children.select.each_with_index { |children, i| i.even? }.collect {|e| e.text}
  end
```


Would love to hear about some of the things you guys learned on your journey to creating the gem. Please comment below.





