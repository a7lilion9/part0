sequenceDiagram
  participant browser
  participant server

  browser->>server: POST https://fullstack-exampleapp.herokuapp.com/new_note
  activate server
  server-->>browser: URL redirect (302)

  Note right of server: The server asks the browser to do a new HTTP GET request to the address defined in the header's Location

  browser->>server: GET https://fullstack-exampleapp.herokuapp.com/notes
  activate server
  server-->>browser: HTML document
  deactivate server

  browser->>server: GET https://fullstack-exampleapp.herokuapp.com/main.css
  activate server
  server-->>browser: the css file
  deactivate server

  browser->>server: GET https://fullstack-exampleapp.herokuapp.com/main.js
  activate server
  server-->>browser: the JavaScript file
  deactivate server

  Note right of browser: The browser reloads the Notes page. The reload causes three more HTTP requests. The browser starts executing the JavaScript code that fetches the JSON from the server

  browser->>server: GET https://fullstack-exampleapp.herokuapp.com/data.json
  activate server
  server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ...]
  deactivate server

  Note right of browser: The browser executes the callback function that renders the notes
