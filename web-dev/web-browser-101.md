# How a Web Browser works 101

As a client/server model, the browser is the client run on a computer that contacts the Web server and requests information. The Web server sends the information back to the Web browser which displays the results on the computer or other Internet-enabled device that supports a browser.

## Main components of a browser

- The User Interface : The user interface is the space where User interacts with the browser. It includes the address bar, back and next buttons, home button, refresh and stop, bookmark option, etc.
- The Browser Engine : The browser engine works as a bridge between the User interface and the rendering engine. According to the inputs from various user interfaces, it queries and manipulates the rendering engine.
- The Rendering Engine :The rendering engine interprets the HTML, XML documents and images that are formatted using CSS and generates the layout that is displayed in the User Interface.
- Networking : Component of the browser which retrieves the URLs using the common internet protocols of HTTP or FTP. The networking component handles all aspects of Internet communication and security. The network component may implement a cache of retrieved documents in order to reduce network traffic. 
- JavaScript Interpreter: It is the component of the browser which interprets and executes the javascript code embedded in a website. 
- UI Backend: UI backend is used for drawing basic widgets like combo boxes and windows. This backend exposes a generic interface that is not platform specific. It underneath uses operating system user interface methods.
- Data Persistence/Storage: This is a persistence layer. Browsers support storage mechanisms such as localStorage, IndexedDB, WebSQL and FileSystem. It is a small database created on the local drive of the computer where the browser is installed. It manages user data such as cache, cookies, bookmarks and preferences.

There are multiple instances of the rendering engine in each tab. 

For details as to how the rendering engine parses what it is sent in the form of a tree is discussed in the references. 

Refs:
- [1](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/#The_main_flow)
- [2](https://medium.com/@monica1109/how-does-web-browsers-work-c95ad628a509)
