# Calibre Browse & Read (CB&R)



[toc]

## About

Calibre-Web is a web app that offers a clean and intuitive interface for browsing, reading, and downloading eBooks using a valid [Calibre](https://calibre-ebook.com) database. 

This specific fork (*Calibre Browse & Read*) has been heavily customized and optimized for use with E-Ink displays, iPads, iPhones, modern Android e-readers and desktop browsers. It strips out legacy theme dependencies, modernizes the UI for touch interfaces, and provides native compatibility with the latest Calibre desktop database schemas.

[![License](https://img.shields.io/github/license/janeczku/calibre-web?style=flat-square)](https://github.com/janeczku/calibre-web/blob/master/LICENSE)

*This software is a fork of [Calibre-Web](https://github.com/janeczku/calibre-web) and licensed under the GPL v3 License.*

## Project History

I started using the excellent Calibre-Web project as a front end to my 40,000+ Calibre eBook collection that I share with family and friends. However, there are some "quirks & features" of its implementation that I found difficult to deal with. Some had to do with the theme layouts of the interface.

For example, when you use the Standard (Light) Theme, the sidebar with the shelves scrolls in unison with the main content window that shows the book covers. That means that, if you want to select a different shelf, you have to scroll all the way back to the top of the web page to see them. The included "caliblur!" theme keeps the shelves stationary while the book covers scroll, however, it has a Plex Media style interface that is difficult for my non-tech savvy family members to navigate.

Additionally, the built-in ePub and PDF readers (the only two formats that I currently support) also left a lot to be desired. Every time a user opens a book, they have to find their way back to where they left off because the reader doesn't remember it for them. There's also no way to dog-ear pages, make highlights and annotations or scroll easily through the book other than using thenext/previous page navigation. The only other option is to download the book to your device and use a separate reader applications such as the excellent **"MoonReader+"**. Again, too complicated for family and friends and also eats up local memory on their tablets for book storage.

What started out as a desire to work out a few of these kinks slowly turned into a wishlist of other features that I thought would turn my customized version of Calibre-Web into my ideal combination eBook Browser/Reader. After working on it for a few months, I wondered whether others would enjoy some of these features as well, so I decided to share back to the community.

## CB&R Features
- **Unified UI & OS-Aware Theming:** The legacy `caliBlur!` theme engine has been completely removed. The application now features a native, unified interface with seamless **Light**, **Dark**, and **Auto (OS-Aware)** modes.
- **E-Ink Optimizations:** A dedicated toggle for E-Ink displays forces a high-contrast monochrome rendering mode, disables UI animations, and sharpens container borders for crisp screen refreshes which are ideal for e-ink devices.
- **Advanced Reader Tracking:** Custom database routing (`ub.py`) seamlessly integrates expanded reader features directly into the internal memory (`app.db`), keeping your main Calibre library pristine:
  - Interactive 5-Star Ratings
  - Mark as Completed tracking
  - Integrated Wishlist management
  - Persistent reading progress, custom user notes and bookmarks
- **Calibre 9.x Native Support:** The backend SQLAlchemy models (`db.py`) have been updated to cleanly support Calibre 9.0+ schemas. Deprecated columns (`isbn`, `flags`, `lccn`) have been permanently removed to prevent 500 Internal Server Errors without requiring manual database hacking.
### Book Browser

Each user has individualized display attributes that are stored in the CB&R database meaning the are portable across multiple devices they may use to browse and read. 

- **Reading Progress Bars:** Each book opened will display a blue bar below the book cover indicating the position of the last page read.
- **Smart Shelves:** After performing an Advanced Search, click on the results page's gear menu to store the results in an existing shelf or create a dynamic <u>Smart Shelf</u> that will re-run the search each time the shelf is selected, thus showing you the most recent results on-demand. Users with Admin privileges can choose to make a Smart Shelf public at the time of creation or via the <u>Edit Shelf</u> option in the Gear menu of the shelf.
- **Star Ratings:** Each user can rate books independently from the Calibre database rating via the <u>Book Details</u> dialog. Users can choose to have the star rating for each book shown as an overlay to the book covers via the gear menu in the book browser. A <u>Ratings</u> shelf allows users to quickly find books they have rated themselves as well as those rated in Calibre's main database.
- **Wishlist:** Each user can tag individual books to be added to a personalized Wishlist via the Book Details dialog. Wishlist books will display a heart overlay to the book covers in the book browser. Additionally, a <u>Wishlist</u> shelf will show all books in the user's wishlist. 
- **Mark as Completed:** Each user can tag individual books as completed via the <u>Book Details</u> dialog. Any book closed on the last page will also be automatically marked as Completed. Completed books will display a `Read` overlay to the book covers in the book browser. Additionally, a <u>Completed</u> shelf will show all books the user has marked as completed. 
- **Book Series Stacks:** Users can choose to show all books that are part of a book series as a collapsed stack via an option in the gear icon in the book browser. When collapsed, clicking on a stack will show all the books in the series. Series Stacks display a badge count indicating how many books are available in the series. Series with only one book will not show a badge. Clicking on them will open the Book Details dialog directly.
- **Box Sets Shelf:** Anthologies and combined series books marked tagged with the keyword <u>Box Set</u> in the Calibre database get automatically added to a unique shelf in the sidebar.
- **Popular Reads:** The old <u>Hot Books</u> page has been converted into a <u>What Others Are Reading</u> page. Books on this page are sorted in descending order based on the number of users who have opened a particular book. An overlay above each book cover shows a count of how many users have opened the book. This overlay can be turned off via an option in the page's gear menu. User's can choose to keep books they look at from being included in these metrics via the <u>Keep Reading Activity Private</u> checkbox in the <u>User Profile</u> page. The profile is accessible by clicking on the person icon at the top right of the interface.
- **Add to any shelf directly from Book Details dialog:** Easily add a book to one or several shelves via a dropdown list without having to exit the Book Details dialog.
- **Navigate to Previous/Next book details:** Buttons above the book cover in the Book Details dialog allow the user to navigate to the next or previous book without needing to close Book Details dialog box between each book.
- **Currently Reading List:** Any book that is open is automatically added to a `Currently Reading` list. This list is always shown in side-scrolling list at top of each Book Browser page.  Additionally, a `Currently Reading` shelf will show all books the user has recently open sorted from most recent to least recent. Clicking on the gear icon allows user to remove books from this list.
- **Bulk Editing of Shelves:** Clicking on the gear icon and selecting Bulk Edit while viewing a shelf allows users to quickly mark multiple books for:
   - Removing from a shelf
   - Moving to another shelf
   - Copying to another shelf
   - Adding to the user's Wishlist.
   - Tagging as completed
- **Resizeable Book Cover Grid:** Use the slider in the top bar to show more or less book covers per screenful.

- **Hierarchical Categories:** Books tagged in calibre using the hierarchical dot-notation (Category.Sub-Category.Sub-Sub-Category) can be displayed in a collapsible tree-view via an option in the Categories Page's gear icon.
- **User-Selectable Dark Mode:** Rather than having the admin select a global option for either Standard or Caliblur! themes,  each user can select **Light**, **Dark**, or **Auto (OS-Aware)** as their preference via the User Profile page. The profile is accessible by clicking on the person icon at the top right of the interface.

### Book Reader Common Features

​	The following options are saved individually for each book per user.

- **Automatically switch to two-page spread on landscape mode** 
- **Force single-page view in landscape mode** 
- **Single page for cover in two-page spread**
- **Bookmarking:** Dog-ear pages you might want to go back to
- **Highlighting:** Select and underline text in one of 4 colors
- **Create annotation text for each highlight**
- **Bookmark and Highlight Navigation**
- **Scrub Bar Navigation:** 
   - Slider to quickly move through book contents
   - Colored round markers to indicate location of colored highlights in text
   - Tick marks to show position of bookmarks in text
   - Start & End navigation buttons
   - Previous & Next Bookmark/Annotation navigation buttons
- **Table of Contents:** Navigation for eBooks that support it
- **Themes:**
   - Auto (OS Setting)
   - Light
   - Sepia
   - Slate (low contrast)
   - Dark
- Last position, Bookmarks, Highhlights and Annotations are stored in central database so they remain visible even if you switch to a different device.

#### ePub Reader-Specific Additional Features

The improved eReader for ePub files includes options to customize the settings listed below. These options are stored per book and per user.
   - Font family
      - Publisher Default 
      - Arial
      - Georgia
      - Times New Roman
      - Verdana
      - Trebuchet MS
      - Courier
      - Comic Sans
   - Font size increase/decrease
   - Word spacing increase/decrease
   - Line spacing increase/decrease
   - Paragraph spacing increase/decrease
   - Left and Right margin size increase/decrease
   - Bold first word of every sentence 

#### PDF Reader-Specific Additional Features

The improved eReader for PDF files includes options to customize the settings listed below. These options are stored per book and per user.

- **Hardware-Accelerated Pan & Zoom Lock:** Maximize your screen real estate by cropping out large white margins. Unlock the viewport, zoom and pan the PDF exactly where you want it, and lock it. The reader will persistently apply your custom crop to every page you turn. Double-tap the Zoom-Lock icon at any time to restore the default size. [^1]
- **Intelligent Theme Inversion:** The Light, Sepia, Slate, and Dark themes don't just change the UI—they mathematically invert, color-shift, and contrast-adjust the actual PDF canvas for comfortable nighttime reading without destroying the page layout. (for true PDF files only. Not for scanned PDFs)
- **Dynamic Page Layouts:** Choose between Single-Page view, Book Spread (cover on its own page), or Continuous Spread layouts. Includes a master toggle to instantly force single-page layouts on landscape screens; handy for use with PDFs that were scanned as double page spreads.
- **Visual Grid Navigation:** A dedicated "Pages" tab generates a grid of book thumbnails. To save device memory, these thumbnails lazy-load only when you scroll to them. The grid actively highlights your current page or two-page spread as you read.
- **Customizable Touch Controls:** Choose between invisible edge-tap zones for distraction-free E-ink reading, or floating hardware-style buttons for ease of use on desktop browsers and to prevent page turn zones from interfering with text highlighting.
- **Options Stored Per-Book:** Your custom zoom-lock crop coordinates, layout preferences, and theme overrides are seamlessly saved to your browser and remembered individually for every single PDF in your library.


## Standard Calibre-Web Features

- Modern and responsive HTML5 interface
- Comprehensive user management with fine-grained per-user permissions
- Multilingual user interface supporting 20+ languages
- OPDS feed for eBook reader apps
- Advanced search and filtering options
- Custom book collection (shelves) creation
- eBook metadata editing and deletion support
- eBook conversion through Calibre binaries
- eBook download restriction to logged-in users
- Public user registration support
- Sync Kobo devices with your Calibre library
- In-browser eBook reading support for multiple formats
- Upload new books in various formats
- Content hiding based on categories and Custom Column content per user

## Installation

### Installation via pip (recommended)

1. **Create a virtual environment:** It’s essential to isolate your Calibre-Web installation to avoid dependency conflicts. You can create a virtual environment by running:
    ```
   python3 -m venv cbr
   ```
2. **Activate the virtual environment**:
   ```
   source cbr/bin/activate
   ```
3. **Install dependencies:** Use pip to install the required packages:
   ```
   pip install -r requirements.txt
   ```
4. **Start Calibre-Web:** After installation, you can start the application with:
   ```
   python cps.py
   ```

## Quick Start
Access Calibre-Web: Open your browser and navigate to:
   ```
   http://localhost:8083
   ```
1. **Log in: Use the default admin credentials:**

   - **Username:** admin
   - **Password:** admin123
2. **Configure Calibre Database:** In the admin interface, set the Location of Calibre database to the path of the folder containing your Calibre library (where metadata.db is located) and click "Save".
3. **Set the default user configuration:** In the admin interface, click on the <u>Edit UI Configuration</u> and then set your preferences in the <u>Default Settings for New Users</u>  and <u>Default Visibillities For New Users</u> sections.
4. **Create New Users:** In the admin interface, click the Add New User button to start building your list of users.
## Requirements

- **Python Version:** Ensure you have Python 3.7 or newer.
- **Imagemagick:** Required for cover extraction from EPUBs.
- **Optional Tools:**
   - **Calibre desktop program:** Recommended for on-the-fly conversion and metadata editing. Set the path to Calibre’s converter tool on the setup page.
   - **Kepubify tool:** Needed for Kobo device support.
   - **jQuery:** v3.5.1
   - **Isotope:** v3.0.6
   - **PDF.js:** v2.16.105 (Modified for Zoom Lock feature)

## Usage Tips

- If using an iPad, you can login to CB&R using Safari and then Select the Add to Home Screen option in the share menu. This will create a web app that will behave like a standard app on your device.
- If you are using an Android device, Fully Kiosk is a great app to use with CB&R. I have configured several cheap tablets this way to give to family members so they can just turn on the device and start using the app without any tech know-how.
- Do you have a huge book library and are looking for something new to read? Click on the <u>Discover</u> page which will load a random selection from your library. As you browse through your book covers, add those that interest you to your wishlist. Refresh the page several times and repeat the process to build up a pared-down collection of books you can then browse by clicking on the <u>Wishlist</u> page. It's a great way to re-discover books that you may have forgotten about.

## Known Issues

- Using the Add to Home Screen option may not actually display the icon on the Home Screen on some iPads. The web app was actually created and can be found by swiping over to the App Library page and searching for "CB&R". In the results, tap & hold the webapp icon and then drag it to the home screen to make it more accessible. This doesn't happen on all iPadOS devices and I haven't tracked down the source of the problem yet. Suggestions are welcome.

## Limitations

- The main limitation of this version is that it is strictly a "connected" application meaning that it requires you to be online while browsing or reading. The reason for this is that the CB&R database is automatically updated in real time each time you move to a new page, highlight text, make an annotation, etc. Other apps wait until you close the book before storing your progress which can result in data loss if you exit ungracefully. You can always download the book and use a different reader if you prefer, but that defeats the purpose of using CB&R.

- Only ePub and PDF formats have been updated to use the integrated reader environment because those are the only two formats I use in my own library. I haven't touched the other readers included with Calibre-Web so I don't know how they work. I might consider updating some of the other readers so they follow the same UI and features if there is enough interest in this project.

- CB&R does not intend to replicate functionality that is best handled by the Calibre application itself. As such, any features that modify the main Calibre library database have been stripped out. If your goal is to remotely add/delete books, change metadata (such as: title, author, description, tags, or series) or modify/add book covers, either do this via the main Calibre app or CB&R is not for you.
  

## Acknowledgements

This code was mostly modified thanks to my trusty assistant Gemini under my direction. I'm very impressed with the results, but I cannot vouch for the efficiency or "correctness" of the code. I was a Pascal, BASIC, C, C++ and 6502 & 68000 Assembly developer in another life, but all these new-fangled web technologies are not my forté. 

**Thank you for considering CB&R!**

