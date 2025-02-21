```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: HTTPS GET exampleapp/spa
    activate server
    server-->>browser: 200 OK return spa html page
    deactivate server

    
    browser->>server: HTTPS GET main.css
    activate server
    server-->>browser: 200 OK returns css stylesheet 
    deactivate server
    browser->>server: HTTPS GET spa.js
    activate server
    server-->>browser: 200 OK returns script 
    deactivate server

    Note right of browser: spa.js script makes request for data.json
    browser->>server: HTTPS GET data.json
    activate server
    server-->>browser: 200 OK
    deactivate server

   Note right of browser: Browser executes an event handler whenever the new notes form is submitted. it renders the updated notes list without refreshing the page and sends the new note to the server.
    
    browser->>server: HTTPS POST {content: "my note", date: "2025-02-21T17:30:08.082Z"} exampleapp/new_note_spa
    activate server
    server-->>browser: 201 response {"message":"note created"}
    deactivate server