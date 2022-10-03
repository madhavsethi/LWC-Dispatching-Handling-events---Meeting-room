What we have learnt:

1. Pass data from Parent Component to Child Component using Public properties.

2. Call Method on child component from Parent Component.



Now we'll learn how Child component can communicate back with Parent Component.

We will do it by firing event from Child Component.



Child component: meetingRoom



When user clicks on tile (child component), we have to dispatch an event which will handled by Parent Component. The tile information has to passed.
------------------
Steps on Child Component:

1. On child component div, add a onclick handler : tileClickHandler()

2. On Child component, define method on js file. From here we will fire an event which will be handled by Parent Component.

To fire event from lwc, we have to use "dispatch event method"



Here tileclick is the event name, when we use it in parent, we have to use it as: on+tileclick = ontileclink! We will also pass payload to this which can be used by Parent Component to perform logic..{detail : this.meetingRoomInfo}



Now, to fire the event, we will use:    this.dispatchEvent(tileClicked)



tileClickHandler(){
        const tileClicked = new CustomEvent('tileclick', {detail : this.meetingRoomInfo, bubbles :true});
 
        this.dispatchEvent(tileClicked);
    }
---------------
Parent Component:

Now we will define Handler on Parent Component.



We can do it by Child Component tag: by using ontileclick.

<c-meeting-room meeting-rrom-info={room} show-room-info ontileclick={onTileSelectHandler}></c-meeting-room>



Now this will be method in js file: onTileSelectHandler



onTileSelectHandler(event){

      const meetingRoomInfo = event.detail;

      selectedMeetingRoom = meetingRoomInfo.roomName;

}

Now on html file... We ware using the property "selectedMeetingRoom"

--------------
Another approach: programmatic approach.

1. Remove handler from the <c-meeting-room>

2. Go to js file.

3. Define Handler for event... in our case we want it at the time of component creation.

4. So, we will define a constructor method... First statement will be super();

5. Define Handler: this.template.addEventListner('tileclick', this.onTileSelectHandler.bind)

[First parameter is the event name(on keyword not required), second is to bind the event Handler]

6. Add bubble property to child.
