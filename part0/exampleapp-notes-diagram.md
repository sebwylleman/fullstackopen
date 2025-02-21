```mermaid
sequenceDiagram
    participant browser
    participant server

    Note right of browser: User submits a "hello" note on page
    activate server
   
    
    server-->>browser: 302 Found response redirects browser to  https://studies.cs.helsinki.fi/exampleapp/notes
    deactivate server

    Note right of server: Server adds the new note to the notes array that it received from the html form

    browser->>server: HTTPS POST new_note
    activate server
    server-->>browser: 200 OK returns html doc new_note
    deactivate server

    
    browser->>server: HTTPS GET notes
    activate server
    server-->>browser: 200 OK returns notes page
    deactivate server
    browser->>server: HTTPS GET main.css
    activate server
    server-->>browser: 200 OK returns css stylesheet 
    deactivate server
    browser->>server: HTTPS GET main.js
    activate server
    server-->>browser: 200 OK returns script 
    deactivate server

    Note right of browser: Browser begings executing main.js which itself makes a GET request to retrieve the updated list of notes from the server

    browser->>server: HTTPS GET data.json
    activate server
    server-->>browser: 200 OK returns the updated notes data in json [{"content": "my-note", "date": "2025-02-21T16:17:24.834Z"},...]
    deactivate server
    Note right of browser: Browser executes an event handler that renders the notes as html lists on https://studies.cs.helsinki.fi/exampleapp/new_notes