# INTE2665 - Week 6 - Network security – part 2

## 6.0.0 Week overview: Network security – part 2
Welcome to Week 6 of Introduction to Cyber Security
This week you’ll look at transport layer security (TSL). The transport layer plays an important role in ensuring end-to-end communication between applications through the use of port numbers. As cybercriminals attack applications using port numbers assigned to them, it’s important to provide security at the transport level, so attacks on the applications can be mitigated. The content from this week along with that in Week 5 will support your ability to complete Assessment 2.
To develop your computer skills, you’ll continue working with packet filtering firewalls (iptables). You’ll be assessed on using these tools in Assessment 2.
Finally, we’ll continue to look at ethics. Your understanding of this important area will also be assessed in Assessment 2.

## What you’ll learn this week
By the end of this week, you’ll be able to:
• explain web security and transport layer security
• describe how ethics and intellectual property apply to cyber security
• analyse web and transport security threats and their solutions
• perform key commands using iptables.

## Week 6 activities
This week you’ll:
• read about web and transport security
• analyse and discuss web and transport layer threats
• watch a video of cyber security professionals discussing key aspects of transport security and reflect on your role in this area
• read about and discuss ethics and cybercrime
• research a real-life intellectual property case study
• practise using commands in iptables.

Week 6 Activity 1: Investigating transport layer security (TLS)

6.1.0 Activity: Investigating transport layer security (TLS)
In this activity you’ll look at transport layer security (TLS). It is the internet standard that relies on the Transmission Control Protocol (TCP) to safeguard network traffic at the transport layer level. You’ll read about TLS before reviewing key terminology and applying your understanding by solving a web security problem using TLS.

6.1.1 Task 1 - Investigate TLS
OVERVIEW
What is TLS?
In this task you’ll read about transport layer security (TLS). This will provide the context for this activity and for Assessment 2.

TLS is a general-purpose service made up of various protocols – for example, handshake protocol, alert protocol and heartbeat protocol. These protocols play important roles in providing secure communication at the transport layer level.

Read - The following will help you learn more about TLS.

Read pages 190-202 (Chapter 6) of:
Network security essentials: applications and standards (Stallings 2017)Links to an external site.
As you read, consider the following questions:
• TLS provides transport level security through the use of various protocols. Why is the functionality broken into the various protocols? Why isn’t it one protocol?
• What is the relationship between a TLS connection and a TLS session, if any?

6.1.2 Task 2 - Explain key concepts in TLS
OVERVIEW
Reviewing transport security terminology
In Task 6.1.1 you read about TLS. In this task you’ll review key terminology in this area. This will consolidate your understanding and prepare you for Assessment 2.
Check your understanding
Review the figure below which shows how the record protocol provides a layer of security for higher-level protocols.

How the record protocol provides a layer of security for higher-level protocols. Source: RMIT Online, adapted from Stallings (2017). Reprinted by permission of Pearson Education, Inc.

Now read the descriptions of each protocol below. Click and drag to match each description to its protocol.
When you’re finished, consider how the protocols work together. You’ll discuss this further in Task 6.1.3.

6.1.3 Task 3 - Discuss a problem about web security
OVERVIEW

What do you think?

In Task 6.1.2 you reviewed the different types of protocols in TLS and considered how they worked together. In this task you’ll discuss the relationship between two of the protocols.

Discuss

Consider the following:
In secure sockets layer (SSL) and TLS, why is there a separate change cipher spec protocol rather than including a change_cipher_spec message in the handshake protocol?

Share your ideas on the discussion board.
Read at least two posts by your peers.
• How similar are their ideas to yours? Question or comment on the strength of their ideas.
Source: Adapted from Problem 6.1 in Network security essentials: applications and standards (Stallings 2017), page 220.

Week 6 Activity 2: Exploring SSL/TLS protocols

6.2.0 Activity: Exploring SSL/TLS protocols

In this activity you’ll examine SSL/TLS protocols. You’ll learn about the relationship between secure sockets layer (SSL) and transport layer security (TLS) protocols, and see how TLS was partially derived from the commercial implementation of SSL.

You’ll read about SSL/TLS protocols and apply your knowledge in discussing SSL/TLS attacks and solving a web security problem using TLS. You’ll also watch a video of cyber security professionals discussing transport security.

6.2.1 Task 1 - Explore SSL/TLS protocols

OVERVIEW

What are SSL/TLS protocols?

In this task you’ll read about SSL/TLS attacks. These protocols have been improved over time to counter new forms of attacks. This will provide the context for this activity and develop your understanding of a key aspect of cyber security.

SSL/TLS attacks can be designed to target individual protocols (e.g., a handshake protocol). In these cases, cybercriminals focus their attention on one part of the communication management at the transport layer level. The success rate of this type of ‘vertical cyber-attack’ can be high.

Read - The following reading will help you learn more about SSL/TLS protocols.

Read pages 205-207 (Chapter 6) of:
Network security essentials: applications and standards (Stallings 2017)Links to an external site.

As you read, consider the following:
• Can an attack on one type of TLS protocol be used on another type of protocol?
• Protocols such as TLS are never considered to have perfect design and implementation; they are always considered ‘works in progress’. Why?

6.2.2 Task 2 - Investigate TLS

OVERVIEW

Where did TLS come from?

In Task 6.2.1 you read about TLS attacks. In this task you’ll watch an expert discuss the background of TLS. This will give you greater understanding of this area and help you prepare for Assessment 3.

Watch the video - Transport layer security (TLS) – Computerphile (15:32 min)

In this video Dr Mike Pound explains more about this internet security protocol.

As you watch, consider the following:
• What are the benefits of TLS?
• Why has it become so popular?

https://youtu.be/0TLDTodL7Lc

Source: Computerphile (2020)

6.2.3 Task 3 - Analyse web threats

OVERVIEW

Countering web security threats

In this task you’ll analyse different web threat scenarios and consider how each could be solved by using a feature of TLS. This will help in understanding the roles of various TLS protocols to counter cyber-attacks for web communications.

Solve the problem

Read the web threat scenarios below.
Consider how each is countered by a particular feature of TLS.
When you’re finished, check your ideas with the sample answers below.

Web threat scenarios:

1. Brute force cryptanalytic attack: An exhaustive search of the key space for a conventional encryption algorithm is undertaken.
2. Known plaintext dictionary attack: Many messages will contain predictable plaintext, such as the HTTP GET command. An attacker constructs a dictionary containing every possible encryption of the known-plaintext message. When an encrypted message is intercepted, the attacker takes the portion containing the encrypted known plaintext and looks up the ciphertext in the dictionary. The ciphertext should match against an entry that was encrypted with the same secret key. If there are several matches, each of these can be tried against the full ciphertext to determine the right one. This attack is especially effective against small key sizes (e.g., 40-bit keys).
3. Replay attack: Earlier TLS handshake messages are replayed.
4. Man-in-the-middle attack: An attacker interposes during key exchange, acting as the client to the server and as the server to the client.
5. Password sniffing: Passwords in HTTP or other application traffic are eavesdropped.
6. IP spoofing: Forged IP addresses are used to fool a host into accepting bogus data.
7. IP hijacking: An active, authenticated connection between two hosts is disrupted and the attacker takes the place of one of the hosts.
8. SYN flooding: An attacker sends TCP SYN messages to request a connection but does not respond to the final message to establish the connection fully. The attacked TCP module typically leaves the ‘half-open connection’ around for a few minutes. Repeated SYN messages can clog the TCP module.

Sample answers:

1. Brute force cryptanalytic attack: The conventional encryption algorithms use key lengths ranging from 40 to 168 bits.
2. Known plaintext dictionary attack: TLS protects against this attack by not really using a 40-bit key, but an effective key of 128 bits. The rest of the key is constructed from data that is disclosed in the Hello messages. As a result, the dictionary must be long enough to accommodate 2128 entries.
3. Replay attack: This is prevented by the use of nonces.
4. Man-in-the-middle attack: This is prevented by the use of public-key certificates to authenticate the correspondents.
5. Password sniffing: User data is encrypted.
6. IP spoofing: The spoofer must be in possession of the secret key as well as the forged IP address.
7. IP hijacking: Again, encryption protects against this attack.
8. SYN flooding: TLS provides no protection against this attack.

Source: Adapted from Problem 6.3 in Network security essentials: applications and standards (Stallings 2017), page 220.

6.2.4 Task 4 - Discuss TLS

OVERVIEW

Functionality of TLS

In this task you’ll discuss types of functionalities when using TLS. This will help you to understand the requirements for secure communication at the transport layer level.

Discuss

Based on what you have learned this week, and without doing research, is it possible in TLS for the receiver to reorder TLS record blocks that arrive out of order? If so, explain how it can be done. If not, why not?
Share your ideas on the discussion board.

Read your peers’ posts and reply to a peer with a different answer to you.
• What evidence did they present? Comment on the strength of their argument. Are you persuaded? Is there an aspect they haven’t considered?

Source: Adapted from Problem 6.4 in Network security essentials: applications and standards (Stallings 2017), page 221.

Week 6 Activity 3: Examining secure socket shell (SSH)

6.3.0 Activity: Examining secure socket shell (SSH)

In this activity you’ll explore secure socket shell (SSH), which is used for remote secure access to systems. You’ll read about SSH and discuss SSH packets. This will help you understand the packet structure and what type of information it uses.

6.3.1 Task 1 - Examine secure socket shell (SSH)

OVERVIEW

What is SSH?

In this task you’ll read about SSH. This will provide the context for this activity and support your work in Assessment 2.

SSH is a special purpose protocol that provides services such as authentication and connection establishment while also providing transport level security.

Read - The following reading will help you to learn more about SSH.

Read pages 208-219 (Chapter 6) of:
Network security essentials: applications and standards (Stallings 2017)Links to an external site.

As you read, consider the following:
• SSH protocol stack provides two types of services: authentication and connection protocols. These two services can only be used one at a time. Why?
• Why is random padding sometimes used with the application packets?

6.3.2 Task 2 - Discuss SSH packets

OVERVIEW

Options for SSH packets use

In this task you’ll discuss specific options when using packet encryption. This will help you to understand the concepts of encapsulation in communication and its role in providing security to the packet in SSL-based communication.

Discuss

For SSH packets, what is the advantage, if any, of not including the mandatory access control (MAC) in the scope of the packet encryption?

Share your ideas on the discussion board.

Read at least two posts by your peers.
• Comment on any possible disadvantages.

Source: Adapted from Problem 6.4 in Network security essentials: applications and standards (Stallings 2017), page 221.

Week 6 Activity 4: Exploring web security

6.4.0 Activity: Exploring web security

In this activity you’ll read about web security and compare threats on the web. Then you’ll participate in a discussion about the advantages and disadvantages of three types of web threat countermeasures. The web is the most widely used application on the internet, so it provides a huge surface area for cyber criminals to mount attacks. Understanding this area is vital to cyber security.

6.4.1 Task 1 - Explore web security
OVERVIEW
Why is web security challenging?

In this task you’ll read about web security. This will provide the context for this activity and support your work in Assessment 2.

Web security is a very challenging task as the web is so widely used and in such various ways; businesses use the web as a platform for service delivery and advertisements, banks use it for online banking, and so on. The web has also become a battleground between cyber criminals and cyber defenders.

Read - The following will help you learn more about web security.
Read pages 188-190, 207-208 (Chapter 6) of:
Network security essentials: applications and standards (Stallings 2017)Links to an external site.
As you read, consider the following:
• What types of cyber threats are on the web and how do these threats evolve?
• What approaches could be adopted to protect applications using the web as a platform? How effective are they?

6.4.2 Task 2 - Compare web threats
OVERVIEW
Analysing types of web threats and solutions
In this task you’ll read about different web threats, identify their types and consider possible solutions. This will help consolidate your learning.
Check your understanding
In Task 6.4.1 you read about possible security threats when using the web. Complete the task below to check your understanding of each threat.
Click and drag to identify the specific type of threat:
• Integrity
• Confidentiality
• Denial of service
• Authentication.

Now consider how you could counter each of these threats. Which type is most difficult to prevent?

Check your ideas with the sample answers below.
Sample answer:
Type of threat Countermeasures
Integrity Cryptographic checksums
Confidentiality Encryption, web proxies
Denial of service Difficult to prevent
Authentication Cryptographic techniques

Source: Adapted from Table 6.1 in Network security essentials: applications and standards, (Stallings 2017), page 189. Reprinted by permission of Pearson Education, Inc.

6.4.3 Task 3 - Discuss web threat solutions

OVERVIEW
Exploring web threat countermeasures
In this task you’ll discuss three types of web threat countermeasures and consider their advantages and disadvantages.
Discuss
Look at the table below. Consider the different approaches to web security.
• What are the advantages of each?
• What are the disadvantages?
Share your ideas on the discussion board. Support your ideas with evidence.
Read at least two posts by your peers.
• Comment on the points they identified. Based on these ideas, which countermeasure seems most effective?

Different approaches to web security. Source: RMIT Online, adapted from Stallings (2017). Reprinted by permission of Pearson Education, Inc.

Week 6 Activity 5: Considering ethics and intellectual property

6.5.0 Activity: Considering ethics and intellectual property

In this activity you’ll examine ethics and intellectual property (IP). IP theft is one of the main cybercrimes committed on the internet. Ethics can play a significant role in educating well-meaning IP misusers.
You’ll read about ethics and intellectual property and research a real-life case study. Finally, you’ll discuss your understanding of the Digital Millennium Copyright Act (1998).

6.5.1 Task 1 - Explore ethics and intellectual property

OVERVIEW

How does ethics relate to IP?

In this task you’ll read about ethics and intellectual property (IP). This will provide the context for this activity and support your work in Assessment 2.

IP is considered a valuable asset to corporations and, as such, it needs to be protected. Cybercriminals can steal IP to monetise it and sell it on the criminal market. Protecting IP can be done by both educating people to uphold IP rules and adopting a framework which can manage and protect the IP.

Read - The following reading will help you to learn more about ethics and IP.

Read pages 6-13 (Chapter 14) of:
Instructor project manual for network security essentials: applications and standards (Stallings 2017)

As you read, consider the following:
• What types of infringements can happen in IP?
• How can digital rights management be used to ensure compliance with IP principles?

6.5.2 Task 2 - Research a case study on IP

OVERVIEW

A controversial case study

In this task you’ll research a case study on intellectual property (IP) using the Digital Millennium Copyright Act 1998. This will give you a better understanding of how the act has been applied.

The Digital Millennium Copyright Act (DMCA) is constantly evolving as technology changes. In 2000, the DMCA was controversially used in a case in the US. Motion Picture Association Agreement (MPAA) attempted to suppress the distribution of De-content scrambling system (DeCSS) programs and derivatives, which could be used to circumvent the copy protection on commercial DVDs.

Research

Search on the internet for a brief description of this case and its outcomes. Think about the following:
• Was the MPAA successful in suppressing details of the DeCSS descrambling algorithm?
• How might the DMCA need to change in the future to adapt to the demands of the future?

Source: Adapted from Problem 14.4 in Instructor project manual for network security essentials: applications and standards (Stallings 2017), page 27.

6.5.3 Discuss ethics and the DMCA

OVERVIEW

Does the DMCA harm creativity?

In this task you’ll discuss the Digital Millennium Copyright Act (DMCA) and fair use and its impacts on creativity. This will help you to understand the challenges of protecting the copyright of creative works.

In Task 6.5.1 you read about how IP can be protected through both educating people and technical solutions. The DMCA provides a means to use technical solutions to automate the process of copyright protection, though as shown in Task 6.5.2, this can be controversial.

Discuss

Think back to what you have researched and read about the DMCA. Consider the following:
• How is fair use of IP permitted by the DMCA?
• What are the concerns raised about the DMCA? Can it harm creativity?

Share your ideas on the discussion board. Support your ideas with evidence. Read your peers’ posts and reply to at least one, commenting on the issues raised.
• Could the Act be altered to protect creativity?

Week 6 Activity 6: Applying packet filtering firewalls (iptables) – part 2

6.6.0 Activity: Applying packet filtering firewalls (iptables) – part 2

Last week you started practising commands using iptables, a packet filtering firewall tool.
This week you’ll continue working with iptables. This tool will be used for Assessment 2, so please bring any problems you are having to this session.

6.6.1 Task 1 - Practise iptables

OVERVIEW

Practising using iptables

In this task you’ll continue to work with iptables. This allows you to practise the direct skills that you’ll need for Assessment 2.

Practise

Go to the Lab manual and navigate to Weeks 5-6 Packet Filtering Firewalls (iptables). Continue to practise:
• adding chains to rules
• viewing line numbers with the rules
• deleting rules
• checking SSH, HTTP and MySQL services
• connecting MySQL server to other computers
• connecting to SSH, web and MySQL servers.
NOTE:
• This is your last week to practise using iptables.
• You may wish to divide your practice time over multiple sessions.

6.6.2 Task 2 - Reflect on using iptables

OVERVIEW

Assessing your progress

In this task you’ll reflect on your use of iptables. This will help you to consolidate your understanding and use of this important tool and will prepare you for Assessment 2.

Reflect

Look back on your work using iptables this week. Write a reflection in your journal considering the following:
• How have you improved since you started practising encryption?
• Which commands do you feel most confident using?
• Which areas would you like to continue to work on after this course?
