## Preface

Web Development is in a weird spot. 
I don't think there's been a better time to build websites and interactive web applications _however_ it's incredibly challenging to
provide guidance for people trying to get a start in web development and don't necessarily have a background in computer science.

The best way I can describe it is that the pieces are all there but it's quite difficult to organise them in a way them in a progressive manner. 

This for me will be a living document that hopefully people wanting to get into web development can get some use from - the purpose
is to guide someone in what's needed to build a dynamic web application. 

## Part 0. What's the end goal?

The end goal for anyone learning web development is to build a web application that serves pages with potentially dynamic content. 

I've intentionally avoided talking about the following technologies in that sentence:

1. HTML
2. CSS
3. JavaScript
4. SQL
5. PHP
6. ASP.NET
7. Go
8. Python

(The list can go on).

The key takeaway for anyone starting out is the less you care about the code and more about the end product the more you'll enjoy web 
(and software) development in general. 

As an developer/engineer/hacker/tinkerer/beginnger you _should_ care about the technology you use in the same way someone picking up a trade
cares what kind of tools they use. Having a preference for a Milwaukee over DeWalt is a very similar conversation to preferring C# over Java - 
the final product does not change however. 

This roadmap will aim to balance the theory of software engineering with the reality that writing web apps is a process of stringing together 
various forms of markup and logic via scripting/backend servers. 

## Part 1. Learn the Markup

There's no way around it - you should learn the fundamentals of HTML and CSS before really getting into JS. 

You've probably heard of JavaScript frameworks such as React, Vue, Svelte etc... They are great in different ways and will provide you
a common way to write _reactive_ web applications. Emphasis on _reactive_ though, reactivity in your web applications is actually on the
tail end of your web development goals and you might find it overwhelming to build counter applications and TODO lists before you learn
how to work with the fundamentals. 

### Learning Goals

Before you move on from working with fundamental HTML and CSS, you should consider trying the following:

* Setup a local development environment and host a local HTML server
  * My recommendation is [VS Code + the Live Server extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer), generally I would avoid just double clicking the HTML files on your computer and opt to instead use basic servers like Live Server to emulate what happens in the real world.
  * If you'd like something more approachable [CodeSandbox](https://codesandbox.io/) or a personal favourite of mine [Glitch](https://glitch.com) are both fantastic web based development environments. Glitch even provides a free hosting model
* Use a CSS Library or Framework
  * Some personal recommendations from me are: [Chota](https://github.com/jenil/chota), [Bootstrap](https://getbootstrap.com) and [Bulma](https://bulma.io/documentation/start/overview/)
  * Libraries such as Tailwind and Material UI actually require a bit more of an understanding of JavaScript so I'd recommend avoiding for now
* Build a personal portfolio/blog
  * This should include multiple HTML pages, CSS that is applied across all pages, common elements like a header
  * If you're wondering why you have to copy and paste so much code, don't worry those abstractions come later
  * [Glitch actually provides a fully functioning template for a personal blog](https://glitch.com/edit/#!/different-wiry-crime?path=README.md%3A1%3A0)
* Feel comfortable with your tools and technology
  * Before reaching for more - understand the point of VS Code, the responsibilities of HTML and CSS, how it all comes together
  * This will make it easier to approach more complicated topics

### Good Resources

* https://learn.microsoft.com/en-us/training/modules/get-started-with-web-development/
  * Guided learning from Microsoft
* https://developer.mozilla.org/en-US/docs/Learn/HTML
  * Fantastic starting point - MDN is the best resource for web development documentation in my personal opinion
* https://youtu.be/PlxWf493en4
  * FreeCodeCamp has excellent intro to HTML videos

## Part 2. Introduce the Dynamic 

There is a common belief that Modern Web Development _requires_ the usage of a frontend framework such as React, Vue, Svelte or Angular (to name a few).
_"Yes and no"_ is my original response to this - whilst you'll find this is the standard experience for many modern web applications the 
reality is the instant need to reach for a frontend framework every time you have to render some form of dynamic content requires an
understanding on how we got to the inception of those frameworks in the first place. 

With the inception of the internet, HTML documents were delivered from a server to a client (the browser).

![Returning Static Content from a Server](https://gist.github.com/assets/7465061/7abfc853-259e-4b0b-845e-d6ae8a36f531)

The ability to render _"dynamic"_ content was limited by the capability of the technology of the time. 
Looking at the above diagram - the best chance you had at dynamic content was by replacing the HTML files on the server with modified
HTML files.

This doesn't scale well and there's very little potential for personalisation - there's no way to provide personalised content, secure 
certain routes to certain users, render potentially endless lists of results. 

Whilst I'm not the biggest fan of [PHP](https://www.php.net/) - it was one of the first and _to this day_ most popular means of 
providing dynamic content to a client. If we had a simple social media app, here's a rough idea of how the call to the server now looks:

![Returning Dynamic Content from the Server](https://gist.github.com/assets/7465061/7aebaca0-2937-4c8d-bd17-d96eca95f5d6)

Asking Copilot to generate some sample code for how this looks, the resulting PHP would look like:

```php
<?php
// Assuming you have a database connection established
// and user authentication implemented

// Get the post ID from the query parameter
if (isset($_GET['id'])) {
    $post_id = $_GET['id'];

    // Fetch the post from the database (you'll need to adjust the SQL query)
    $sql = "SELECT * FROM posts WHERE id = ?"; // Change table and column names as needed
    $stmt = $pdo->prepare($sql);
    $stmt->execute([$post_id]);
    $post = $stmt->fetch(PDO::FETCH_ASSOC);

    if ($post) {
        $user_id = $post['user_id']; // Get user ID
        $content = $post['content']; // Get post content
        $created_at = $post['created_at']; // Get post creation timestamp

        // You can format the timestamp as needed (e.g., using date() function)
        $formatted_date = date('F j, Y', strtotime($created_at));

        echo "<div class='post'>";
        echo "<p>Posted by User #$user_id on $formatted_date:</p>";
        echo "<p>$content</p>";
        echo "</div>";
    } else {
        echo "<p>Post not found.</p>";
    }
} else {
    echo "<p>Invalid request. Please provide a valid post ID.</p>";
}
?>
```

The key takeaway from all of this - the client receives a _rendered HTML template_ which is then rendered in your browser. This is 
the defining difference between a web SITE and a web APP - the web application can provide a dynamic experience based on various inputs.
Another thing to note, PHP is not the only way of doing this. Unlike the browser which historically only supports HTML, CSS and JS there are many backend/API frameworks in a variety of languages. I can confidently say every semi-popular to popular programming language has a backend framework: [Python has Django (as well as many others)](https://www.djangoproject.com/), [Java has Spring Boot](https://spring.io/web-applications), [C#/.NET have ASP.NET](https://dotnet.microsoft.com/en-us/learn/aspnet/what-is-aspnet), [Go has Gin](https://github.com/gin-gonic/gin) and even PHP which by design can create web apps without any framework has [Laravel to provide some helpful abstractions and batteries included functionality](https://laravel.com/),

There are some limitations to this _serverside_ approach to web app development:

1. Individual chunks/parts/components of pages can't change without a hard refresh (although there's been efforts to overcome this such as [HTMX](https://htmx.org/), [LiveWire](https://laravel-livewire.com/), [Blazor Server](https://learn.microsoft.com/en-us/aspnet/core/blazor/hosting-models?view=aspnetcore-8.0#blazor-server) to list a few)
2. Transitioning between pages/views in a serverside web app requires a full page change (think the browser loading bar spinning, the whole page refreshing)
3. All processing needs to happen on your server, you end up footing the bill for 100% of the user experience (this is a double edged sword)

JavaScript is the means of solving these issues, which is where frontend frameworks come into play:

![Frontend Rendering](https://gist.github.com/assets/7465061/b4f8a2a9-01b4-4e42-b627-f3600e53426b)

This same application now returns a payload (usually in JSON form) which the _client browser_ will take and render dynamic UI with. 
The benefits to this are:

1. The web app can change without explicit reloads of the page - creating a feeling similar to a desktop or mobile app.
2. Components can "lazy load" - parts of the page can be loaded before others allowing for different areas of the page to be prioritised
3. Pages can be gesture driven - swiping elements to achieve actions, drag and drop, dismissing modals and notifications to name a few
4. The client takes on some of the load of your web app - their device is now in charge of rendering the page and your API/Backend is purely for fulfilling requests for data

AngularJS 1.0 (one of the first pioneers of client driven web apps) came out in 2010; in just under 15 years we've learnt of some of the 
drawbacks of the SPA (Single Page App) driven approach:

1. With the introduction of so many dependencies to render these pages - clients end up downloading massive "bundles" JavaScript just to run the page. Whilst caching alleviates this, in serverside app rendering the server is the main place to store dependencies.
2. Decision fatigue - too many frontend frameworks which all try to achieve the same goal but slightly different, for newcomers especially this is a tough learning experience.
3. There is a lot of challenge in writing performant web applications that are heavily driven by JavaScript - it's gotten easier however there are many ways with these frameworks to "shoot yourself in the foot" and bad web applications are often plagued with loading spinners, laggy user experience and on budget/low-end devices some apps may be close to unsuable.
4. It is harder to write applications that are SEO friendly & accessible to those with disabilities as pages are constantly changing and there's often no final "loaded" state in a frontend web app.
5. The architecture of these applications all things considered is generally more complicated with more points of failure - what used to be just a web server that served dynamic HTML is now a Web API that is often a separate service from your UI which provides data to the UI service which is then rendered for the browser.

This is not to say frontend web frameworks are bad as right now I'd say there's never been a better time to be a frontend developer. I think it's just worth understanding that for many websites they can overcomplicate a simple design; it's worth understanding the journey of web app architectures and that whilst it's not the _"default"_ anymore server rendered web apps have a tonne of benefits.

### Learning Goals

* Build a basic server rendered web app - for example it could be something that takes in a path such as `/hello?name=Alex` and in return _"Hello Alex"_ should be printed on the page.
** [The PHP tutorial could be used as a starting point for this](https://www.php.net/manual/en/tutorial.php)
** You're going to be learning JavaScript anyway so try using the [NodeJS package Hono which has HTML rendering](https://hono.dev/docs/helpers/html)
** As a .NET developer [I can recommend trying Blazor](https://dotnet.microsoft.com/en-us/learn/aspnet/blazor-tutorial/intro) which tries to mix both serverside and clientside into a single framework

### Good Resources

* [I built 10 web apps... with 10 different languages](https://youtu.be/FQPlEnKav48)
  * Great overview of being able to use a variety of frameworks to achieve the same backends
* [What it's like to run HTMX in production](https://hamy.xyz/labs/2024-04_htmx-in-production)
  * Overview of the mysterious middle ground of HTMX
* [MVC Explained](https://www.codecademy.com/article/mvc)
  * Whilst the pattern is not as popular anymore, it's still the bread and butter of web frameworks such as Ruby on Rails and there is merit in understanding why MVC emerged as the most popular way to structure web apps for a very long time. 

## Part 3. Sprinkle in the Reactive

We've reached the point where acknowledge our JavaScript overlords. [The joke is there's a new JavaScript framework every week](https://youtu.be/cuHDQhDhvPE), there's merit to this but in 2024 the decision making process is getting easier. 

Looking at the [2023 Stack Overflow Developer Survey](https://survey.stackoverflow.co/2023/#section-most-popular-technologies-web-frameworks-and-technologies) - the top three frameworks that pop up are:

1. React (Next.js I will talk about soon as being part of this)
  *  "The library for web and native user interfaces" - Developed by Meta
  *  Pioneered an approach of developing web applications where HTML is defined within JavaScript files using a markup called HTMX
  *  By far the most popular of the three - to the point that many ideas established in React and JSX itself are shared across other frameworks
  *  Components are written using a function based, composable syntax
2. Angular
  * Developed by Google, not to be confused with the original Angular.js 1.0 release which differs greatly and was the biggest framework before react
  * Emphasis on a "batteries included" approach to web development - frameworks like React allow for various approaches to the same problem however Angular is _opinionated_ in its design and will tell you how to do things rather than provide the option.
  * Components are written as classes rather than functions
3. Vue.js
  * "The Progressive
JavaScript Framework" - developed independently of a big tech corporation with Evan You as the key developer.
  * Tries to walk the line between being a full framework that an entire website is written and a smaller framework that can be added onto an existing website 
  * Supports both a function based and object based approach to defining components

Each of these frameworks are equally as usable for building frontend web applications - their priorities and approach to achieving this is what sets them apart.

For this document we'll be focusing on discussing how to get started with React but it should be straight forward to switch in a different framework entirely if you'd prefer. 

The [React documentation's quick start](https://react.dev/learn) is great for as a starting point, including the tic-tac-toe tutorial. 

As you work through these tutorials there'll be a tonne words that gets thrown around and it can be confusing, before moving ahead let's rapid fire a few:

### NodeJS 

The defacto way to run JavaScript outside of the browser; used to run development environments, host servers, build websites. NodeJS and JS are not different, NodeJS is a way to run JavaScript 
on a server rather than in your browser.

Fun fact is NodeJS is actually built on top of Chrome's JavaScript Engine "V8" - this means that when you run Node it's essentially just spinning up a component of Chrome.

### NPM 

Node Package Manager. Installed with NodeJS and can be used to work with NodeJS projects and install NodeJS dependencies.

You'll often see commands such as `npm i some-package` - this adds the package to your NPM project which can then be used in your code.

Often times your projects will support `npm run dev` for running a Dev server for your code.

### Build Tool

JavaScript is a scripting language, you don't need to "build it" however when you have lots of JavaScript dependencies and technologies you need a build tool to convert source JavaScript into output JavaScript. 
With React for example, a build tool is almost always required as JSX is not the same as JavaScript and must be converted to vanilla JavaScript via a build tool. 

Examples of build tools are Vite, Webpack, Parcel, Rollup (there's heaps, you don't need to learn all of them).

### TypeScript

JavaScript by default is a "loosely typed" language - this does not mean much when beginning to learn the language but as you work with more complex codebases it will make sense why it's used.
I am a big Typescript advocate, [there's fantastic videos explaining why](https://youtu.be/EUlM3wx546o?si=9NLbAxST9ij7GxDm), for now just know that Typescript is something that is very quick
to learn when you're more accustomed to writing JavaScript.

The key things to keep in mind for React are:

1. React rewards you for writing good JavaScript - all React components are just functions
2. React components are best when they're cohesive and loosely coupled (like all good code)
3. React uses the same attributes as vanilla HTML and JS, `onclick` against a `<button>` in React is very similarly invoked as it would with vanilla JS.
4. React by design is state driven and it's worth understanding this. The UI changes when the state of the UI changes, that's it. Explore the `useState` hook and how it drives "re-renders" of your app

On the topic of the various react frameworks, we'll go through the role of "meta-frameworks" such as Next.js and Remix later. 
My recommendation is follow guides that use build tools such as Vite ([MDN's tutorial seems excellent](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started))
as this keeps things simple and lets you focus on learning React.

### Learning Goals

Completing the mentioned tutorials should be plenty, my other recommendation is to try implementing the same learning goals.

For React specifically consider how you'd work with [lists of data](https://react.dev/learn/rendering-lists),the various ["hooks"](https://react.dev/reference/react/hooks) and generally the whole ["Describing the UI" section is insightful.](https://react.dev/learn/describing-the-ui)

In Part 4 we'll try to put together data from a server into your frontend UI - for now focus on building Todo lists, forms, navigation bars, dynamic lists etc...

## Part 4. Present your Data

The last piece missing in your web development journey is the way we actually persist the data that drives our applications. It was alluded to in Part 2 that often times what differentiates
a web site from a web app is the presence of a persistent, dynamic, data store behind the web app.

The PHP snippet below is an example of querying a database:

```php
$sql = "SELECT * FROM posts WHERE id = ?"; // Change table and column names as needed
$stmt = $pdo->prepare($sql);
$stmt->execute([$post_id]);
$post = $stmt->fetch(PDO::FETCH_ASSOC);
```

In the example above we use SQL (`$sql`) which is then prepared into a statement (`$stmt`) and after being ran with `execute`, the result is assigned to the `$post` variable. 

There's no absolutes in programming but you're pretty safe to assume that most web applications in their most basic form look like this:

![basic web app architecture](https://gist.github.com/assets/7465061/1f440cab-5cca-4b97-9459-82eee1452515)

When working with server rendered apps like the provided PHP sample, the UI and API can be considered merged together but 
generally you'll find most sites these days opt for the frontend (UI) and backend (API) to be separate components.

I'll go more into this in Part 5 - but this "stack" is a pretty foolproof to build consistently structured web applications
with their still being plenty of choice of what you use for the individual components. 

Typically, the _database_ component has been an SQL database variant such as [MySQL](https://www.mysql.com), 
[Microsoft SQL Server](https://www.microsoft.com/en-au/sql-server/sql-server-2022) or 
[PostgreSQL](https://www.postgresql.org) however there are plenty of alternatives. Like with Web Frameworks - this can lead to a feeling of decision paralysis and it becomes even harder to decide as you begin to look into other paradigms of data access such [NoSQL databases](https://aws.amazon.com/nosql/) and fully managed backends such as [Firebase](https://firebase.google.com).

The best approach you can take in my view - learn SQL and the rest will make sense with time. Any of the three 
mentioned above will fit the bill (I'm currently loving Postgres the most) but by understanding where SQL fits in
and how crucial a part it is of your application it will set you up for success as you review other storage options. 

[The fundamentals can be explained in 100 seconds](https://youtu.be/zsjvFFKOm3c), there are plenty of free 
tutorials online to go through the setup and once you're comfortable you can explore how applications connect to [SQL using Object Relational Mappers](https://www.youtube.com/watch?v=4QN1BzxF8wM&t=60s&pp=ygUOb3JtcyBleHBsYWluZWQ%3D). Once you understand this, you can then finalise it by returning that data from your API for consumption in your UI.

This is lot to process all at once, but my recommnendation is start with SQL. You don't _need_ an API to work with 
SQL, similar to how you PHP and C# are lanaguages which can build backends, SQL is the language used for querying 
databases. Downloading a client such as [DBeaver](https://dbeaver.io) or [Azure Data Studio](https://learn.microsoft.com/en-us/azure-data-studio/quickstart-postgres) is a great way to get started writing SQL queries once you've setup an server.

To recap all of this with an opinionated example, if I chose C# as the language for my first API and I had to connect it to a database I would:

1. Install Postgres locally (https://www.postgresql.org/download/)
2. Install a tool such as DBeaver, Azure Data Studio or PGAdmin to interact with the database (I'll go with PGAdmin as it's the specific tool for Postgres so less fuss to setup)
3. I'd then spend a good amount time with the database and learn the fundamentals, [Design Database with PostgreSQL](https://www.codecademy.com/learn/paths/design-databases-with-postgresql) seems like a great Codecademy course to learn this information for free. 
4. Lastly, I'd learn how to query the database from my C# application. Writing a google query as simple as ["postgres C# tutorial" yieled this fantastic article](https://michaelscodingspot.com/postgres-in-csharp/) which goes over how to write commands against the database by hand using an ORM such as Dapper or how to use Entity Framework to generate schema for the database in code. 
5. To expose this via an API in C#, [this tutorial from Microsoft is the last resource I'd review](https://learn.microsoft.com/en-us/aspnet/core/tutorials/min-web-api?view=aspnetcore-8.0&tabs=visual-studio)

There's _a lot_ to learn when it comes to connecting all these components together however find comfort in knowing these motions are the same for every language. With the understanding of how to learn this in C#, it becomes much easier if I wanted to switch in a new database or a different language. 
If I wanted to write the same example above in a language such as Go, really all that needs to change is step 4 (potentially opting for an ORM such as [GORM](https://gorm.io/docs/)) and instead using a framework such as [Gin](https://gin-gonic.com/docs/quickstart/) for the API.

### Learning Goals

* Implement the above example; you can choose to use C# or if you'd prefer a challenge try to piece together the same outcome with another language
* Understand how to CRUD with SQL - Create, Read, Update and Delete. This is the bread and butter of building any API
* You might not even need a server to learn SQL, try [SQLite](https://www.sqlite.org) which is a _file based_ version of SQL that is used heavily in Mobile and Desktop Apps. For smaller apps it is a fantastic replacement for SQL will save you spinning up a dedicated server to learn the basics of the language. [Dbeaver has a driver](https://github.com/dbeaver/dbeaver/wiki/Database-driver-SQLite) for SQLite it is supported by pretty much every programming language. 

### Good Resources

* [7 Database Paradigms](https://www.youtube.com/watch?v=W2Z7fbCLSTw)

## Part 5. What's next?

When you step back and look at this all, there's a lot to web development. The complexity of getting into the industry is what prompted the creation of this document in the first place. 

My recommendation is to take each one of stages and really get to understand their place in the web development landscape. 
Find other tutorials and resources, the benefit of such a constantly evolving field is that the resources available to you for learning are also constantly developing. 

This final section is a rapid fire of concepts and technologies that you'll need to understand as you become a web developer - do not take this as gospel (to be honest that goes for most of this document). Software engineers love having opinions, myself included, and this section is heavily driven by what _I want_ from web development.

### Do I need TypeScript?

Probably - it's a hard one because I personally would prefer someone learning how to create web apps avoid using additional layers of abstraction on top of JavaScript. 

JavaScript is a pretty shity language that you almost should experience in all its shittiness to fully learn it. There's quite a few existing languages that pitch themselves as being a way to avoid writing JS. [Coffeescript](https://coffeescript.org) was one of the first big attempts to make it happen. 
You also have languages such as [Dart](https://dart.dev/interop/js-interop) and [Gleam](https://gleam.run/news/v0.16-gleam-compiles-to-javascript/) which out of the box aim to compile to machine code but also support JavaScript interoperability. 
WebAssembly in the browser has allowed for languages such as Rust and C# to compile to your browser as a target. This has allowed frameworks to circumvent JavaScript entirely and is the foundation of frameworks such as [Blazor](https://dotnet.microsoft.com/en-us/learn/aspnet/blazor-tutorial/intro).

These are all great pieces of technology (bar CofeeScript) - however I find that avoiding JavaScript in web 
development provides very diminishing returns. You will end up writing JavaScript if you try to avoid it on the 
web, it might be for to integrate with a component or to use a shared library for your specific use case but I do think if your intention is to not write JS at all then this falls apart pretty easily. 

All this is to say - this is why TypeScript is so popular. TypeScript as the name implies is an attempt to add types to JavaScript, a language with no explicit type system. 
[The explanation for JS developers is a good introduction to the language](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html), generally the idea with TypeScript is whilst it _can't_ add runtime checks for types out of the box during the development phase you can avoid shooting yourself in the foot as much. You can write as much TypeScript as you feel like writing - the following lines of code are both valid forms of TypeScript. 

```ts
let name = "Alex";
let nameButTyped: string = "Alex";
```

The `name` variable will have the type of `string` because it can expect that from the assigned value of "Alex", whilst the bottom variable is asserting it upfront. Play around with it, read the docs, I love TypeScript as someone from a strongly typed language background and believe in larger codebases it comes in clutch.

### Meta-Frameworks?

You've probably heard of NextJS, Remix, Nuxt, Sveltekit, SolidStart etc... If not, congratulations you're happier than most web devs. 

Modern web dev heavily pushes you to use these frameworks as they help get you started with building quality web apps. These are known as _meta-frameworks_, they're frameworks on-top of frameworks and they all have similar goals:

1. Provide logical defaults and conventions for development (directory structure, routing, media resolution, tooling, SEO, hosting etc...)
2. Support different rendering modes for your web applications including generating static sites, pre-rendering frontend code on a server for better performance, hosting websites on cloud specific platforms such as AWS Lambda and CloudFront Edge functions
3. Add "Backend For Frontend" (BFF) capabilities for more complicated websites that need it

These add some very much needed opinions to libraries/frameworks such as React (NextJS & Remix), Vue (Nuxt), Svelte (Sveltekit) and Solid (Soldstart) - all of these UI solutions out of the box do not enforce you to write code in a specific way despite there often being a best practice that can be followed.

When working in a team, I love these frameworks! However it's good to know that you don't have to use them and often times for smaller apps tools like Vite will suffice a lot of the time.

I like NextJS even if newer versions are making some _interesting_ decisions with regards to how you deploy it and changes to their router (see pages router to app router discussions on the internet).
I'd also consider Remix as I find the model to be a bit more straightforward. 

[Astro](https://astro.dev) is also a fantastic framework for building websites that only need _a little_ bit of reactivity. 

There's lots of them and it's worth trying to pick one up with your next project to cut out some of the tougher parts of settings things up.