# 🦈 Fiche Outil : Wireshark

## 📌 Utilité

- **Qu'est-ce que c'est ?** L'analyseur de paquets (sniffer) open source le plus populaire du marché. Il permet de capturer et d'inspecter en temps réel le trafic circulant sur un réseau informatique à un niveau granulaire.
- **Cas d'usage principal :** Analyse de trafic réseau, diagnostic de pannes, rétro-ingénierie de protocoles et investigation numérique (Network Forensics) lors d'incidents de sécurité.

## ⚙️ Fonctionnement & Caractéristiques Clés

!Wireshark empty interface

Wireshark empty interface

!image.png

- **Capture en mode promiscuité :** Permet à une interface réseau de capturer l'ensemble des paquets visibles sur le segment réseau, et non seulement ceux qui lui sont destinés.
- **Moteurs de décodage avancés :** Capable d'interpréter des milliers de protocoles (HTTP, DNS, TLS, SMB, TCP/UDP, etc.) du modèle OSI couche 2 à couche 7.
- **Moteur d'export & d'analyse :** Possibilité d'exporter des objets (fichiers, images) directement à partir d'un flux de données capturé.

## ⚡ Utilisation

#### 🛠️ Colouring packets

Wireshark has two types of packet colouring methods: temporary rules that are only available during a program session and permanent rules that are saved under the preference file (profile) and available for the next program session. You can use the "right-click menu" or **"View --> Coloring Rules"** menu to create permanent colouring rules. The **"Colourise Packet List"** menu activates/deactivates the colouring rules. Temporary packet colouring is done with the "right-click menu" or **"View --> Conversation Filter"** menu.

!Default permanent colouring

Default permanent colouring

#### 🛠️ Traffic Sniffing

🔵 Blue **"shark button"** —> start network sniffing (capturing traffic)

🔴 Red button —> stop the sniffing

🟢 Green button —> restart the sniffing process.

 The status bar will also provide the used sniffing interface and the number of collected packets.

#### 🛠️ Merge PCAP files

Wireshark can combine two pcap files into one single file. You can use the **"File --> Merge"** menu path to merge a pcap with the processed one. When you choose the second file, Wireshark will show the total number of packets in the selected file. Once you click "open", it will merge the existing pcap file with the chosen one and create a new pcap file. Note that you need to save the "merged" pcap file before working on it.

#### 🛠️ View files details

Knowing the file details is helpful. Especially when working with multiple pcap files, sometimes you will need to know and recall the file details (File hash, capture time, capture file comments, interface and statistics) to identify the file, classify and prioritise it. You can view the details by following "**Statistics --> Capture File Properties"** or by clicking the **"pcap icon located on the left bottom"**.

#### 🛠️ Packet details

You can click on a packet in the packet list pane to open its details (double-click will open details in a new window). Packets consist of 5 to 7 layers based on the OSI model. We will go over all of them in an HTTP packet from a sample capture. The picture below shows viewing packet number 27.

!image.png

Each time you click a detail, it will highlight the corresponding part in the packet bytes pane.

!image.png

!image.png

**The Frame (Layer 1):**This will show you what frame/packet you are looking at and details specific to the Physical layer of the OSI model.

!Wireshark - layer 1

**Source [MAC] (Layer 2):**This will show you the source and destination MAC Addresses; from the Data Link layer of the OSI model.

!Wireshark - layer 2

**Source [IP] (Layer 3):**This will show you the source and destination IPv4 Addresses; from the Network layer of the OSI model.

!Wireshark - layer 3

**Protocol (Layer 4):**This will show you details of the protocol used (UDP/TCP) and source and destination ports; from the Transport layer of the OSI model.

!Wireshark - layer 4

**Protocol Errors:**This continuation of the 4th layer shows specific segments from TCP that needed to be reassembled.

!Wireshark - protocol error

**Application Protocol (Layer 5):**This will show details specific to the protocol used, such as HTTP, FTP,  and SMB. From the Application layer of the OSI model.

!Wireshark - layer 5

**Application Data:** This extension of the 5th layer can show the application-specific data.

!Wireshark - application data

#### 🛠️ Packet Navigation

- **Packet numbers**

Wireshark calculates the number of investigated packets and assigns a unique number for each packet. This helps the analysis process for big captures and makes it easy to go back to a specific point of an event.

!Wireshark - packet numbers

- **Go to packet**

Packet numbers do not only help to count the total number of packets or make it easier to find/investigate specific packets. This feature not only navigates between packets up and down; it also provides in-frame packet tracking and finds the next packet in the particular part of the conversation. You can use the **"Go"** menu and toolbar to view specific packets.

!Wireshark - go to packet

- **Find packets**

Apart from packet number, Wireshark can find packets by packet content. You can use the **"Edit --> Find Packet"** menu to make a search inside the packets for a particular event of interest. This helps analysts and administrators to find specific intrusion patterns or failure traces.

There are two crucial points in finding packets. The first is knowing the input type. This functionality accepts four types of inputs (Display filter, Hex, String and Regex). String and regex searches are the most commonly used search types. Searches are case insensitive, but you can set the case sensitivity in your search by clicking the radio button.

The second point is choosing the search field. You can conduct searches in the three panes (packet list, packet details, and packet bytes), and it is important to know the available information in each pane to find the event of interest. For example, if you try to find the information available in the packet details pane and conduct the search in the packet list pane, Wireshark won't find it even if it exists.

!Wireshark - find packets

- **Mark Packets**

Marking packets is another helpful functionality for analysts. You can find/point to a specific packet for further investigation by marking it. It helps analysts point to an event of interest or export particular packets from the capture. You can use the **"Edit"** or the **"right-click"** menu to mark/unmark packets.

Marked packets will be shown in black regardless of the original colour representing the connection type. Note that marked packet information is renewed every file session, so marked packets will be lost after closing the capture file.

!Wireshark - mark packets

- **Packet comments**

Similar to packet marking, commenting is another helpful feature for analysts. You can add comments for particular packets that will help the further investigation or remind and point out important/suspicious points for other layer analysts. Unlike packet marking, the comments can stay within the capture file until the operator removes them.

!Wireshark - packet comments

- **Export packets**

Capture files can contain thousands of packets in a single file. As mentioned earlier, Wireshark is not an IDS, so sometimes, it is necessary to separate specific packages from the file and dig deeper to resolve an incident. This functionality helps analysts share the only suspicious packages (decided scope). Thus redundant information is not included in the analysis process. You can use the **"File"** menu to export packets.

!Wireshark - export packets

- **Export objects (Files)**

Wireshark can extract files transferred through the wire. For a security analyst, it is vital to discover shared files and save them for further investigation. Exporting objects are available only for selected protocol's streams (DICOM, HTTP, IMF, SMB and TFTP).

!Wireshark - export objects

- **Time display format**

Wireshark lists the packets as they are captured, so investigating the default flow is not always the best option. By default, Wireshark shows the time in "Seconds Since Beginning of Capture", the common usage is using the UTC Time Display Format for a better view. You can use the **"View --> Time Display Format"** menu to change the time display format.

!Wireshark - Edit Time Display Format

!Wireshark - time display format

- **Expert info**

Wireshark also detects specific states of protocols to help analysts easily spot possible anomalies and problems. Note that these are only suggestions, and there is always a chance of having false positives/negatives. Expert info can provide a group of categories in three different severities. Details are shown in the table below.

| **Severity** | **Colour** | **Info** |
| --- | --- | --- |
| **Chat** | **Blue** | Information on usual workflow. |
| **Note** | **Cyan** | Notable events like application error codes. |
| **Warn** | **Yellow** | Warnings like unusual error codes or problem statements. |
| **Error** | **Red** | Problems like malformed packets. |

Frequently encountered information groups are listed in the table below. You can refer to Wireshark's official documentation for more information on the expert information entries.

| **Group** | **Info** | **Group** | **Info** |
| --- | --- | --- | --- |
| **Checksum** | Checksum errors | **Deprecated** | Deprecated protocol usage |
| **Comment** | Packet comment detection | **Malformed** | Malformed packet detection |

You can use the **"lower left bottom section"** in the status bar or **"Analyse --> Expert Information"** menu to view all available information entries via a dialogue box. It will show the packet number, summary, group protocol and total occurrence.

!Wireshark - expert info

#### 🛠️ Packet filtering

- **Apply as filter**
- **Colourise conversation**
- **Prepare as filter**
- **Apply as column**
- **Follow stream**
- **Simple display filter queries**
