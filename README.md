# CaseyBook Lab Part 2

## In Which We Talk About Presentational Components...

Welcome back, friends! It's time to cut `App.js` down to size! If you're just joining us, feel free
to clone down the project, it has all of the code from Part 1.

If you remember where we left off, we had our initial component, `App.js` with state, and an initial
`profile` object containing our profile data. This is all fine and dandy, the problem, though, is
that as we build out more complexity, our `App.js` component will start to become difficult to 
manage. Instead, let's start by creating a folder, `components`, that will house all of our custom
components. There are a wide variety of ways to arrange the file structure in a React project, 
instead of debating the various pros and cons, I'm going to stick with a components folder with 
all of the custom components inside, and depending on where you work / what other tutorials you are 
following, just remember that following the path of the imports is your best friend! We'll get into 
that in just a moment.

So let's go to our terminal (if you cloned down this project don't forget to cd into the directory
and run `npm install` to install all of the React packages!) and create the directory and then the 
file.

```bash
mkdir src/components
touch src/components/Profile.js
```

Let's navigate to our new file and scaffold out a bare bones React components. Start by importing
React, create a function (since we won't need state we don't need to create a class component. When
possible keep all components as function components, they're much smaller and load much faster!),
and export! All together it will look like this:

```javascript
import React from 'react';

const Profile = () => {
  return (

  )
}

export default Profile;
```

Let's put in an `<h2>` element and give it some text inside the return statement. The final (for now)
Profile component will look like this:

```javascript
import React from 'react';

const Profile = () => {
  return (
    <div>
      <h2>Profile Page</h2>
    </div>
  )
}

export default Profile;
```

Alright, so we have our `App.js` component as our entry point, and our `Profile.js` component. Let's
now import our `Profile` componet in `App.js`, and send some information to it!

Start with the import. At the top of `App.js` add in `import Profile from './components/Profile';`
and then in your `App.js` JSX, replace your `<h1>` with your `<Profile />` and voila! Your profile
component is now rendering!!
