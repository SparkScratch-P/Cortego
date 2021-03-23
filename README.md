# Cortego

Host your personal Chat room from ur own Server
---
 **Cortego** is an easy-to-use customable group chat engine for ur website.
 
 UI Customized for use in ***Company Discussions, Friends Online Group chat, Team Planning, Broadcasts, etc.***

 An example for Cortego is available at https://sparkscratch-p.github.io/cortego/ ( Cloud Variables wont work )
 Default websocket : `ws://localhost:3000/` (not active)


## How to use Cortego?

The UI
---

 Cortego cant be used as it is not readily available in this repo.
   This repository has all the coding and assets for setting up Cortego in its `main` branch.
  
   The room name is **Chat Room** by default.
  
   The Default Admin name for Cortego is **Sparkscratch_P**
   
   Once this name is entered, it asks for an Admin password
   
   The Admin Password by default is **12345**
   
   In stead, when any other name is entered in its place, it asked for a general Password. Enter **qwerty** to enter the room.
  
  Once entered as an Admin, you can do the following things by clicking on the `security` button on top-left of screen.:
  
  - Change default Password
  - Change Admin Password
  - Change Room name (enter <10 chars for best results)

The Hosting
---

To host **Cortego** , first *fork* this repository. All u need to do is , go to the `index.md` file in ur repo's `main` branch, and navigate the following lines: 

```
 const noop = () => null;
  let cloudHost = "ws://localhost:3000/";
  let ws;
  function openConnection() {
    try {
      ws = new WebSocket(cloudHost);
    } catch (err) {
      console.warn(err);
      return;
    }
    ws.onmessage = onMessage;
    ws.onopen = onOpen;
    ws.onclose = onClose;
  }
  function onMessage(e) {
    e.data.split('\n').forEach(message => {
      if (message) {
        const { name, value } = JSON.parse(message)
        vm.postIOData('cloud', {
          varUpdate: {name, value}
        });
      }
    });
  }
  function sendData(data) {
    data.user = DESIRED_USERNAME;
    data.project_id = PROJECT_ID;
    ws.send(JSON.stringify(data) + '\n');
  }
  function onOpen() {
    sendData({method: 'handshake'});
  }
  function onClose() {
    setTimeout(openConnection, 500);
  }
  
  function postError(err) {
    vm.postIOData('cloud', {
      varUpdate: {
        name: CLOUD_PREFIX + 'eval error',
        value: err.toString()
      }
    });
  ]
  ```

 Now, in the line that says ` let cloudHost = "ws://localhost:3000/";` , change the `ws://` value to ur own personal Websocket Server.
 
 
 Create a Wesocket
 ---
 
 Quide Available by SheepTester [here](https://github.com/SheepTester/primitive-cloud-server#primitive-cloud-server)


### Enjoy with ur Team and Friends!

# Head Onn!

























