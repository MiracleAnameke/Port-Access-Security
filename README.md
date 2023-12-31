# Port Access Security

## Lab Overview
This lab focuses on understanding and utilizing NetBus, a tool that functions as a Remote Administration Tool (RAT) for both legitimate and malicious purposes. Through this lab, you'll explore how NetBus operates and its implications for security by setting up a scenario involving a hacker computer (Windows 7 VM) and a victim computer (Windows Server 2008 VM).

## Lab Requirements
- VMware images: Windows 7 (as the hacker's computer) and Windows Server 2008 (as the victim's computer).
- Both systems' firewalls disabled.
- Administrator access on both VMs.

## Lab Setup
- **Win7 Hacker Computer**: Assign IP address `10.81.10.1/24` and set Network Adapter to Host-only mode.
- **Win2008 Victim Computer**: Assign IP address `10.81.10.2/24` and set Network Adapter to Host-only mode.
- **Connectivity**: Verify connectivity between both VMs using ping.
- **Folder & File Setup**: On Win2008, create a folder with your FOLusername and a file containing your full name.
- **NetBus Installation**: Find and run `patch.exe` on the victim computer and `netbus.exe` on the hacker computer.

## Lab Procedure & Screenshots

### Step 1: Verifying patch.exe is Running
**Task**: Ensure that the NetBus server component (`patch.exe`) is running on the victim machine.
- **Action**: Open Task Manager on Win2008, go to the Processes tab, and look for `patch.exe`.
- **Slide 01**: Screenshot of Task Manager showing `patch.exe` running.
    
    <img src="https://i.imgur.com/G0nsC4y.png" height="400px" width="auto" alt="Task Manager showing patch.exe"/>
    

### Step 2: Verify Open Ports with netstat
**Task**: Confirm that `patch.exe` has opened the default port for NetBus (TCP 12345).
- **Action**: Open command prompt on Win2008 and enter `netstat –nao`. Look for the port 12345 in the list.
- **Slide 02**: Screenshot of the command prompt showing the output of the `netstat –nao` command.
    
    <img src="https://i.imgur.com/HrLD3iU.png" height="400px" width="auto" alt="netstat showing TCP 12345"/>
    

### Step 3: Verify Startup with msconfig
**Task**: Check that `patch.exe` is set to start automatically using the System Configuration utility.
- **Action**: On the victim computer, execute `msconfig`, navigate to the Startup tab, and verify that `patch.exe` is listed.
- **Slide 03**: Screenshot of the Startup tab in the System Configuration Window.
    
    <img src="https://i.imgur.com/G0nsC4y.png" height="400px" width="auto" alt="System Configuration Startup Tab"/>
    

### Step 4: Using NetBus Features - File Manager
**Task**: Use the File Manager in NetBus to interact with the file created earlier.
- **Action**: From the NetBus control panel on Win7, use File Manager to locate and interact with the folder named after your FOLusername on the victim's computer.
- **Slide 04**: Screenshot of the File Manager showing the folder.
    
    <img src="https://i.imgur.com/A8rzhWA.png" height="400px" width="auto" alt="NetBus File Manager"/>
    

### Step 5: Using NetBus Features - Message Manager
**Task**: Send a custom message to the victim's computer.
- **Action**: From the NetBus control panel, use the Msg Manager to send a message saying "Hello my name is <your name>".
- **Slide 05**: Screenshot of the message appearing on the victim's computer.
  
    <img src="https://i.imgur.com/2Qr4Yep.png" height="400px" width="auto" alt="NetBus Message Manager"/>
    

### Step 6: Set New Listening Port and Password
**Objective**: Change the default listening port of the NetBus server and set a new password for access.
- **Steps**:
    1. Stop `patch.exe` on the victim's computer using Task Manager.
    2. Execute `Patch /port:20016` in the NetBus directory to set a new listening port.
    3. Restart `patch.exe`.
    4. Connect to the new port from the hacker's computer.
- **Slide 6**: Screenshot showing the successful connection attempt to the new port with the password prompt window.
  
  <img src="https://i.imgur.com/rLGHDSM.jpg" height="400px" width="auto" alt="New Listening Port and Password Prompt"/>

### Step 7: Verify Listening Port Change
**Objective**: Confirm the change of the listening port on the victim computer.
- **Steps**:
    1. Verify `patch.exe` is running with the new port settings on the victim's computer.
    2. Execute `netstat –nao` to view active ports.
- **Slide 7**: Screenshot of the `netstat –nao` output, showing the new listening port active.

  <img src="https://i.imgur.com/YiD7C2h.png" height="400px" width="auto" alt="Verify Listening Port Change"/>


### Step 8: Verify New Listening Port via Netbus
**Objective**: Ensure the new listening port is operational and the victim computer is accessible through it.
- **Steps**:
    1. Connect to the victim's computer using the new port via the NetBus client on the hacker's computer.
- **Slide 8**: Screenshot showing the `netstat –nao` command output on the victim's computer, confirming the established connection from the hacker's computer using the new port.

<img src="https://i.imgur.com/vMOpO0t.png" height="400px" width="auto" alt="Netstat Command Showing New Listening Port"/>

### Step 9: Confirm Remote Access via New Port
**Objective**: Validate remote access functionality through the newly set port and password.
- **Steps**:
    1. Perform remote activities using the NetBus client connected to the new port to confirm control over the victim's computer.
- **Slide 9**: Screenshot showing the NetBus client successfully connected and interacting with the victim's computer using port 44177.

  <img src="https://i.imgur.com/H29d4PE.jpg" height="400px" width="auto" alt="Confirming Remote Access via New Port"/>
  

  ## Conclusion
This lab provides hands-on experience with the NetBus tool, demonstrating the ease of system compromise and control. It emphasizes the importance of understanding and securing systems against such RAT tools, highlighting the need for robust security measures and user awareness.

