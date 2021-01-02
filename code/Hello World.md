Hello World. :)

This website is an attempt at a fully in-the-cloud development stack. The FE code is on codepen, in a project that can be deployed. The intent is to put cloudflare in front of it for SSL cert and caching. The content is in github, it is a bit backwards to have the *content* be under version control, but not the page! I hope codepen offers github/bitbucket integration in the future. I lost some work because I opened an old tab that overrode work I had done since!

This stack is fully in the cloud- no npm install, can edit the code as easy as the posts from anywhere. No databases to maintain. You can tell I thought of this project before the pandemic started, and I am stuck at home anyway! Oh well, it was fun to mess around.

For ~100 lines as of writing, I am surprised at how fully featured I was able to get it in this little break I had to work on it. It supports multiple blogs in one site, direct linking, pages, social links, automatic sitemap in the footer, pagination for posts. Showdown provides the markdown to HTML. It retreives a manifest.json file, index.json files, and the markdown files themselves over jsdelivr client side.

One snag I ran into that I would like to resolve next is the index.json file- right now manually maintained by me- it would be nice for CI to run and automatically create it. 

I picture the final workflow to be **just** adding a new file in github. 
