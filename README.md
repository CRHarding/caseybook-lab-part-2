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

Now the fun begins, we now want to send our profile information from state down to our Profile component. This brings up the subject of props. State is data that lives on the component itself, props are passed from a parent component to a child component. We'll be seeing a lot more of props in future labs!

You can treat the `<Profile />` element that we wrote in our JSX like a JavaScript function and pass data through to it, very similar to the `()` in function calls. It looks like this:

```javascript
<Profile data={this.state.profile} />
```

What react does is it parses through the values inside of the `<` and `/>` tags and creates an object for us that it calls `props`. The values before the equals sign become the keys in this object, the values after the equals sign become the values in the object. So, up above, React is going to create a props object and go like so:

```javascript
const props = {
  data: this.state.profile
}
```

We're now sending data to our Profile component, let's now accept that data and then render it to the page!

Go to your Profile.js file and add in `props` to the function expression:

```javascript
const Profile = (props) => {
```

What we can do now is take the code from our App.js:

```javascript
<p>{this.state.profile.username}</p>
<img src={this.state.profile.image} alt="user" />
<p>{this.state.profile.about}</p>
```

and move it to Profile.js:

```javascript
import React from 'react';

const Profile = () => {
  return (
    <div>
      <h2>Profile Page</h2>
      <p>{this.state.profile.username}</p>
      <img src={this.state.profile.image} alt="user" />
      <p>{this.state.profile.about}</p>
    </div>
  )
}

export default Profile;
```

If you save the file you'll notice...an error! This is because our Profile.js file doesn't know anything about state, instead it's getting the data via props from our `App.js` file! Let's update our values:

```javascript
import React from 'react';

const Profile = (props) => {
  return (
    <div>
      <h2>Profile Page</h2>
      <p>{props.data.username}</p>
      <img src={props.data.image} alt="user" />
      <p>{props.data.about}</p>
    </div>
  )
}

export default Profile;
```

Phew, much better. So now we have our `App.js` file which has all of our data, and it passes it down to our `Profile.js` file which is only concerned with displaying the data. If we update values in state, our `Profile.js` file will correctly update the UI to reflect the changing data!

Before we let you rock and roll on your own for a bit, let's update our `App.js` state and add in company information that we'll display in a footer component. So, in `App.js`'s constructor, 
let's update state:

```javascript
this.state = {
  profile: {
    username: "CRHarding",
    image: "http://images6.fanpop.com/image/photos/32800000/Thor-thor-32844898-1024-768.jpg",
    about: "Lorem ipsum dolor sit amet..."
  },
  companyInfo: {
    name: "CaseyBook",
    creator: "Casey Harding",
    social: [
      { facebook: "facebook.com" },
      { twitter: "twitter.com" },
      { instagram: "instagram.com" }
    ]
  }
}
```

(You can put whatever you want in the companyInfo value, I just chose this because...)

So we now have a new state value which has a key of `companyInfo` and a value of an object, what I want you all to do is to create a new presentation component, `Footer.js`, and pass the values in state down as props, and then display them! Take 30 minutes to give it a shot.

<details>
  <summary>Struggling? Remember to import React at the top of the file and to export the component! Your initial component should look like...</summary>

```javascript
import React from 'react';

const Footer = () => {
  return (
    <h2>Footer!</h2>
  )
}

export default Footer;

```
</details>

<details>
  <summary>Struggling? Remember to import your new component in App.js and to include it in your JSX! The updated App.js should look like...</summary>
  
```javascript
import React, { Component } from 'react';
import './App.css';

import Profile from './components/Profile';
import Footer from './components/Footer';

class App extends Component {
  constructor() {
    super();

    this.state = {
      profile: {
        username: "CRHarding",
        image: "http://images6.fanpop.com/image/photos/32800000/Thor-thor-32844898-1024-768.jpg",
        about: "Lorem ipsum dolor sit amet..."
      },
      companyInfo: {
        name: "CaseyBook",
        creator: "Casey Harding",
        social: [
          { facebook: "facebook.com" },
          { twitter: "twitter.com" },
          { instagram: "instagram.com" }
        ]
      }
    }
  }

  render() {
    return (
      <div className="App">
        <Profile data={this.state.profile} />
        <Footer />
      </div>
    );
  }
}

export default App;
```
</details>

<details>
  <summary>Struggling? Remember to pass props down to your Footer.js file and to render out some information! The updated App.js and Footer.js should look like...</summary>
  
App.js:
```javascript
import React, { Component } from 'react';
import './App.css';

import Profile from './components/Profile';
import Footer from './components/Footer';

class App extends Component {
  constructor() {
    super();

    this.state = {
      profile: {
        username: "CRHarding",
        image: "http://images6.fanpop.com/image/photos/32800000/Thor-thor-32844898-1024-768.jpg",
        about: "Lorem ipsum dolor sit amet..."
      },
      companyInfo: {
        name: "CaseyBook",
        creator: "Casey Harding",
        social: {
          facebook: "facebook.com",
          twitter: "twitter.com",
          instagram: "instagram.com"
        }
      }
    }
  }

  render() {
    return (
      <div className="App">
        <Profile data={this.state.profile} />
        <Footer info={this.state.companyInfo} />
      </div>
    );
  }
}

export default App;
```
  
Footer.js:
```javascript
import React from 'react';

const Footer = (props) => {
  return (
    <div>
      <h2>{props.info.name}</h2>
      <h3>{props.info.creator}</h3>
      <a href={props.info.social.facebook}>Facebook</a>
      <a href={props.info.social.twitter}>Twitter</a>
      <a href={props.info.social.instagram}>Instagram</a>
    </div>
  )
}

export default Footer;
````
</details>

If you finished the above early, might as well rock and roll! Create a new state key value pair called `headerInfo`, a new Component called `Header.js`, and get exporting, importing, and displaying some data! This is more freeform, you can take this in whatever direction you want. 


<details>
  <summary>If you want to see how I'd tackle it, click the triangle to the side...</summary>
  
App.js
```javascript
import React, { Component } from 'react';
import './App.css';

import Profile from './components/Profile';
import Footer from './components/Footer';
import Header from './components/Header';

class App extends Component {
  constructor() {
    super();

    this.state = {
      profile: {
        username: "CRHarding",
        image: "http://images6.fanpop.com/image/photos/32800000/Thor-thor-32844898-1024-768.jpg",
        about: "Lorem ipsum dolor sit amet..."
      },
      companyInfo: {
        name: "CaseyBook",
        creator: "Casey Harding",
        social: {
          facebook: "facebook.com",
          twitter: "twitter.com",
          instagram: "instagram.com"
        }
      },
      headerInfo: {
        cta: "The Only Social Media Site You'll Ever Need!",
      }
    }
  }

  render() {
    return (
      <div className="App">
        <Header info={this.state.headerInfo} />
        <Profile data={this.state.profile} />
        <Footer info={this.state.companyInfo} />
      </div>
    );
  }
}

export default App;
```
  
Header.js:
```javascript
import React from 'react';

const Header = (props) => {
  return (
    <div>
      <p>{props.info.cta}</p>
    </div>
  )
}

export default Header;
```
</details>
  
Final update...don't be lazy, get some styling in there!

Alright! If you hit any walls feel free to exapand for some code snippets above. We now have a two component application, hold onto your seats, next up is using an API call to grab data from a random user API to grab some user data to `fake` some friends! Onwards and upwards!



<details>
  <summary>Shhhhhhhhhhhh</summary>
    Full solution code for this lesson found here...https://github.com/CRHarding/caseybook-lab-part-3
</details>
