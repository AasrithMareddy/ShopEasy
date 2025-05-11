**ShopEasy**

ShopEasy is an iOS shopping aggregator application that allows users to
search, compare, and purchase products from various e-commerce platforms
through a unified, clean interface. The app is built using SwiftUI and
Firebase, following the MVVM architecture.

**App Flow and Screens**

**1. Login Screen**

![](media/image1.jpeg){width="0.9187620297462817in"
height="1.9738451443569554in"}![](media/image2.jpeg){width="0.9083333333333333in"
height="1.9831878827646545in"}![](media/image3.jpeg){width="0.8666666666666667in"
height="1.9498600174978127in"}![](media/image4.jpeg){width="0.9083333333333333in"
height="1.987538276465442in"}![](media/image5.jpeg){width="2.4095406824146983in"
height="1.0277777777777777in"}![](media/image6.jpeg){width="1.9916666666666667in"
height="0.9958333333333333in"}![](media/image7.jpeg){width="2.0416666666666665in"
height="1.0289763779527559in"}![](media/image8.jpeg){width="1.9666666666666666in"
height="1.0334448818897637in"}![](media/image9.jpeg){width="4.033333333333333in"
height="1.4583333333333333in"}![](media/image10.jpeg){width="0.95in"
height="2.056149387576553in"}

On launch, users see the Signup/Login screen. It features the ShopEasy
logo and options to sign in with Google or continue as a guest. Google
Sign-In is handled via Firebase Authentication, allowing secure and
seamless login. Once authenticated, the app navigates to the Home Page.

**2. Home / Browse Screen**

![](media/image11.jpeg){width="1.1166666666666667in"
height="2.4842913385826773in"}![](media/image12.jpeg){width="1.125in"
height="2.4889457567804025in"}

The Home Page displays a feed of product listings fetched from multiple
vendors. A search bar is available at the top, and each product is shown
with an image, title, and price. Users can scroll through items and tap
on a product to see more details. The cart icon in the navigation bar
shows the current number of items. Product data is stored in Cloud
Firestore, allowing the app to read and write items and listen for
real-time updates as inventory or listings change.

**3. Search Functionality**

![](media/image13.jpeg){width="1.2127143482064742in"
height="2.6333333333333333in"}![](media/image14.jpeg){width="1.1833333333333333in"
height="2.6355457130358704in"}

Tapping the search icon opens the Search screen. Users can enter
keywords to find specific products across all vendors. As the user
types, the app queries the local product data (and can be extended to
query an API) and displays matching results in a list below. Each result
shows a product thumbnail, name, and price. The search results update
dynamically as the user refines their query.

**4. Product Detail Screen**

![](media/image15.jpeg){width="1.0742563429571304in"
height="2.3740463692038496in"}![](media/image16.jpeg){width="1.075in"
height="2.3730599300087487in"}

When a user selects an item from Home or Search, they navigate to the
Product Details view. This screen shows a larger product image, detailed
description, price, and vendor name. An Add to Cart button lets users
add the item to their shopping cart. The view also includes a Visit
Vendor button which opens the vendor's website (using a web view or
external browser) for purchasing. The details and images are loaded from
Firestore, ensuring up-to-date information.

**5. Cart Screen**

![](media/image17.jpeg){width="1.203992782152231in"
height="2.6666666666666665in"}

The Cart view lists all products the user has added. Each entry displays
the product name, price, quantity, and subtotal. Users can adjust
quantities or remove items. The total price is calculated at the bottom.
A Checkout button triggers redirection to the vendor's checkout page for
all items in the cart. The cart contents are stored in Firestore under
the user's account for persistence across sessions.

**6. Vendor Redirection**

![](media/image18.jpeg){width="1.1833333333333333in"
height="2.6150984251968503in"}

Finally, ShopEasy handles Vendor Redirection. When the user checks out,
the app opens the vendor's online store page (via SafariView or similar)
to complete the purchase. This hands off the final transaction to the
vendor.

**Admin Panel**

![](media/image19.jpeg){width="1.2792224409448818in"
height="2.808333333333333in"}![](media/image20.jpeg){width="1.253429571303587in"
height="2.7916666666666665in"}![](media/image21.jpeg){width="3.2416666666666667in"
height="1.7407895888013998in"}![](media/image22.jpeg){width="3.2333333333333334in"
height="1.7201935695538058in"}

Only users with the admin email ID can access this screen. The admin
panel allows uploading mock product data into Firebase. This panel is
essential for managing the product inventory and is structured to
support future integration with real product data scraped from
e-commerce platforms.

**Firebase Integration**

ShopEasy uses Firebase as its backend platform. Firebase Authentication
is used for user login, including Google Sign-In (OAuth) for quick
account
access[firebase.google.com](https://firebase.google.com/docs/auth/ios/start#:~:text=You%20can%20use%20Firebase%20Authentication,in%20to%20your%20app).
Cloud Firestore is the primary database: it stores product listings,
user profiles, and cart data. The app reads and writes to Firestore,
leveraging its real-time sync to update UI instantly as data
changes[firebase.google.com](https://firebase.google.com/codelabs/firestore-ios#:~:text=In%20this%20codelab%20you%20will,You%20will%20learn%20how%20to).
A custom *Manager* layer (e.g. FirebaseManager) encapsulates all
Firebase calls; ViewModels interact with this manager rather than
calling Firebase directly. This separation aligns with the MVVM pattern:
ViewModels request data through managers, and managers handle
authentication and database logic.
