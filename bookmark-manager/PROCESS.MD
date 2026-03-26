# Process Document For Bookmark Manager

## What I Built and Why
I built a bookmark manager that allows users to add bookmarks with a note and title. It also lets the users tag the bookmarks. 
The app also has a search feature which lets users filter the search by tags.

## My Build Process

### What I asked the agent to do
I asked it to build the core layer first, which had the following features: display a list of bookmarks, add a new bookmark (URL and title), persistant bookmarks saved in browser storage. 

I then did some hands on testing to make sure that I could add a bookmark, see the list, and that the list persisted when I reloaded the page. 

Once I verified that functionality from the core layer, I then asked the tool to build the next 5 layers; notes and tags, edit and delete, tag filtering, search, and polish. 

Polish was basically a dark mode and collapsing form. The form would collapse until the user clicks the "add" button. 

### What worked on first try 
The core layer, notes/tags, edit/delete, and search all worked on the first prompt.
### What I had to fix or adjust
Surprisingly, the tag filtering failed on the first try. I had expected that tag filtering would work like an `AND` -- I expected to be able to click on multiple tags and that links that had the corresponding tags would stay in the list. This did not work, and I had to ask for it as a follow up prompt. 

### Any verification failures and how I resolved them
See above -- unexpected behavior on the tag filtering. Thinking this through, my assumption wasn't in the initial `DESIGN.md` document, so I shouldn't be surprised that it didn't appear. If I wanted that functionality I should have been explicit about it. 
## What I learned
My background is in data science/statistics not as a full stack web developer, and I didn't know anything about localstorage in the browser. I learned about it during the guild tutorial. 
## Known issues
After the "polish" layer of development, the resulting UI has borders around the tags that make the tags hard to see. I think there should be some kind of contrasting line around the tags to increase visibility. 

Regarding the tag filtering, I think there should also be an option to use the tag filter as an `OR` instead of only `AND`.


