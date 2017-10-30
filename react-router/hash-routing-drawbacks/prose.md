
## Hash-Based Routing Drawbacks

In the previous lesson, you learned about hash-based routing. Let's use an analogy to think about how routing works. Imagine you want to read a book, so you go to the library.

Depending on what you're looking for there two ways you can find what you're looking for:
1. You walk in and tell the librarian you would like to read something by Maya Angelou. The librarian pulls up a cart with all 100,000 of his letters. Then the librarian asks you which title you would like to read. You tell them, and they pull out and hand you the book.
2. You walk in and tell the librarian the title of the book you would like to read. They grab that specific book and hand it to you.

The first scenario would be hash-based routing. Using the hash, you pull the main URL of the website (in the analogy - the cart of all things written by the author). After the server grabs the code, the browser pulls the fragment identifier (specifying exactly which page you want) out of local storage and sends a query back to the server. Then, the server returns the exact page matching the query.

The second scenario is resource routing. You send the full URL with query string to the server and it fetches the exact resource you require.
They work in different ways, but both methods work.

There's also a third scenario. Suppose tell the librarian the name of the author you'd like to read. They come back with the cart, ask you title of the book, but is speaking a language you don't understand. Your inability to communicate with the librarian is similar to what happens when the browser you're using isn't running JavaScript. The returned code can't be read, which means you end up with a broken link.

### Hash It Out

Why use hash routing at all? The hash-bang was originally intended as a means to help search engines index dynamically loaded AJAX websites. It can help to speed up page loading time, since the browser will load the static HTML content of the base URL once, then download the dynamic content related to the fragments as they are requested. If the bulk of your site is made up of static HTML (with dynamic content being a minor component) then hash routing will help your pages load faster.

Another issue with using hash-based routing is that the URL fragments don't appear in browser history. 
The browser loads the page faster because it ignores URL fragments where the base URL is the same, and loads the HTML from the cache. A side effect of this is that URLs that differ only in fragments will appear as one entry in browser history, which means users can't hit the back button to navigate on your page. They also can't bookmark a specific page that's pulled from a fragment.

### Conclusion

![mp-newt-got-better.jpg](https://tiy-learn-content.s3.amazonaws.com/3c6ced62-mp-newt-got-better.jpg)

There are other ways of routing that we can use to give the best possible user experience. One such example we have already covered, using the HTML5 History API.

### More Reading

Before search engines people used 'crawling' URLs to be able to search for things on the web. In 2011, when Gawker/Lifehacker redesigned their sites with hashbangs resulting in site-wide outages. You can read about it in detail [here](https://www.wired.com/2011/02/gawker-learns-the-hard-way-why-hash-bang-urls-are-evil/) but the gist is that the URL with the hashbang depends on JavaScript to retrieve the content, and when the JavaScript failed to load properly, every URL on their page was broken.

#### References

[Broken Links](http://www.tbray.org/ongoing/When/201x/2011/02/09/Hash-Blecch)

[Breaking the Web with HashBangs](http://isolani.co.uk/blog/javascript/BreakingTheWebWithHashBangs)
