---
layout: post
title:      "Aftermarket Shop: React/Redux Project with Rails API"
date:       2018-08-08 06:00:39 +0000
permalink:  aftermarket_shop_react_redux_project_with_rails_api
---

Full disclosure: upon realizing that I had nearly completed the final project in the Flatiron course, the first song I listened to this morning was *The Final Countdown* by Europe. It seemed appropriate, given the distance covered from day one. Plus, 80's power-ballads are better than caffeine when it comes to energizing for that final push.

This final project was meant to encompass everything learned in the course, from setting up a Rails API to creating a React/Redux client app and incorporating acquired knowledge of Ruby, JavaScript, HTML, and CSS. I felt it was an appropriate and true test of the course material and challenged me to look back over the last few months and utilize all my memory and resources. It feels like I’ve come a long way, though I know coding is a life-long journey of learning.

For the React/Redux app, I was inspired by my wife’s recently-developed hobby of selling vintage items on Etsy. She enjoys visiting thrift stores and hunting for great value items (i.e. Coach handbags for $5) and decided to start restoring them as needed and reselling them.

I created essentially a stripped-down Etsy clone ("Aftermarket"), designed as an e-commerce app specifically for unique items. In other words, once a product is sold, there's no additional stock available for other buyers.

First, I generated the React-Rails app using [create-react-app](https://github.com/facebookincubator/create-react-app) and began setting up the API on the back-end in Rails, using the User, Product, Cart, and CartProduct models to access the database. The User API uses 2 layers of additional nesting for the cart and products:
```
{
  id: 1,
  token: "47a995c7-c2c5-4488-9ab8-f2fc191da138aft18test",
  email: "test@aftermarket.test",
  first_name: "Brennan",
  last_name: "Heisler",
  address: "1234 Main St",
  city: "Durnsville",
  state_initials: "IN",
  zip: 12345,
  cart: {
    id: 1,
    products: [
      {
        id: 1,
        name: "Crossbody Dark Green Leather Purse / G.H. Bass",
        img_thumbnail: "http://heislercreative.com/demos/aftermarket/crossbody_thumb.jpg",
        price: 70,
        sold_out: false
      },
      {
        id: 4,
        name: "Brown Heels with Bow / Size 8.5 US Women's / NEW never worn",
        img_thumbnail: "http://heislercreative.com/demos/aftermarket/brown_shoes_thumb.jpg",
        price: 25,
        sold_out: false
      }
    ]
  }
}
```
While most of the API data are in string format, I needed to display product photos as well. I decided to follow the common production standard of storing the images on an external server. Normally this would be something like Amazon S3, but in this case I uploaded them to my personal site in order to be able to use the image urls.

Once the API was sorted, I began developing the client-side in React. I used [semantic-ui-react](http://react.semantic-ui.com/) as a styling framework, and since I was new to it, I first played around with their various layout components and stubbed out the general look of the app. Overall, I was very impressed with the amount of features available out-of-the-box, although I also added my own CSS for the fine details. Then, I set to work on filling out the actual content and functionality for each page and custom components.

For the main App component, I used a fair amount of conditional rendering to change access to components when logged in/out.
```
<Router>
        <div className="App">
          { this.props.token && <LoggedInMenu /> }
          { !this.props.token && <LoggedOutMenu /> }
          <Divider hidden />
          <Route exact path="/" component={ProductsPage} />
          <Route exact path="/products" component={ProductsPage} />
          <Route path={'/products/:productId'} component={ProductShow} />
          <Route path={'/confirmation'} component={OrderConfirmation} />
          { this.props.token && <Route exact path="/account" component={Account} /> }
          { !this.props.token && <Route exact path="/login" component={Login} /> }
          { !this.props.token && <Route exact path="/signup" component={Signup} /> }
          { this.props.token && <Route exact path="/cart" component={Cart} /> }
        </div>
      </Router>
```
The menu set is determined by login status, so I used both a LoggedInMenu and LoggedOutMenu component for the appropriate navigation. In order to prevent direct access to these routes through the browser's address bar, I used conditional rendering based on the existence of a user's token in the Redux state.

Most of the app's components remained internally stateless, but I did end up connecting several to the Redux store to make use of the current user, products list, and current product data. This also allowed me to create and easily access the various fetch actions needed to connect to the API.

The app uses [redux-persist](https://github.com/rt2zz/redux-persist) to keep a copy of the store in the browser's local storage. While a live production version would likely use session storage (perhaps through use of JWT) to allow for timeouts, I found that persisting the store locally helped immensely when developing, as it avoided resetting the entire app every time I made an edit. It also allows the user to completely clear their user data from the store for a secure log out.

With the main functionalities working, I went back through and fine-tuned more visual and practical behaviors, such as disabling the 'Add to Cart' button when a product is already in the cart.
```
//AddToCart.js

constructor(props) {
    super(props)
    if (props.productIds.includes(parseInt(props.productId))) {
      this.state = { buttonDisabled: true }
    } else {
      this.state = { buttonDisabled: false }
    }
  }
...
handleSubmit = (e) => {
  e.preventDefault()
  this.props.actions.addToCart()
  this.setState({ buttonDisabled: true })
}
...
render(){
  return(
    <div>
      <Form id="add-to-cart" onSubmit={this.handleSubmit}>
	     <Button primary type='submit' disabled={this.state.buttonDisabled}>Add to Cart</Button>
      </Form>
    </div>
```
At the end, I was able to confirm that there is a lot going on behind the scenes of e-commerce web apps, as seamless as they may seem in daily use. While a production iteration of this app would obviously need to include features like online payments (preferably through a secure third-party like PayPal to keep data off the local server) and order tracking, being able to build both the front and back ends from the ground up was a great learning experience and a worthy challenge!
