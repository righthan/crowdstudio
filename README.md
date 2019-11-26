# CrowdStudio

## Who are we?
Crowdstudio is a streamer-viewer communication system which delivers messages to the streamer that represent the consensus of opinions between viewers while preserving the context-relevance.


## System Structure
- Main page : `src/pages/index.vue`
- Major components : Note that the component files reside in `src/components` directory.

  - Chat Stream : `ChatStream.vue`
    - This renders all chats from the viewers.
  - Chat Input : `SendMessage.vue`
    - A viewer can send a message to either all viewers or the streamer.
  - Message Status : `Status.vue`
    - This shows the popularity of the message sent by the viewer.
  - Message Voter : `MessageVoter.vue`
    - A viewer can upvote the special message sent by the other viewers.
  - Rank : `RankMessageSpecial.vue`
    - The special messages are sorted according to (# of upvotes / # of upvote requests).



## Development
### Setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).




