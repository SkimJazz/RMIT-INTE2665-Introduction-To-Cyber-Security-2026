# 1.0.0 Week overview: Cyber security concepts

Approx. 9 hours to complete all tasks in this week


## Welcome to Week 1 of Introduction to Cyber Security

This course will provide you with a blend of theoretical knowledge and practical cyber security 
computer skills. In each week of learning, you’ll read about and apply theory through various 
tasks that will ensure you understand the fundamental issues in cyber security. Then, in the 
final activity of each week, you’ll practise and develop your hands-on computer skills.

This week you’ll be introduced to the three key cyber security concepts of confidentiality, 
integrity and availability (the CIA triad). They are used to determine the cyber security 
objectives for organisational assets (e.g., data, digital infrastructure). To understand the 
need for a systematic approach in defining cyber security requirements, you’ll also reflect 
on computer security challenges faced by organisations. You’ll study Open Systems Interconnection (OSI) 
security architecture, which helps in devising approaches (security mechanisms and security services)
to counter different cyber-attacks.

The key concepts explored during Weeks 1 and 2 will provide a solid foundation for all your 
work on this course, and will be vital for you to complete the assessments.

To develop your computer skills, you’ll install the operating system Kali Linux, which is the main 
platform used on this course. You’ll complete tasks using Kali Linux in both Assessment 1 and 
Assessment 2. This week you’ll start by practising basic commands in Kali Linux.


## What you’ll learn this week

- Explain the security requirements of confidentiality, integrity and availability
- Describe the challenges faced by computer security professionals
- Evaluate different categories of cyber-attacks that can threaten the security of computer systems
- Explain how OSI security architecture helps to develop approaches for cyber security.


## Week 1 activities

- Watch an interview with cyber security professionals and consider your role in cyber security
- Examine the CIA triad and evaluate levels of security
- Read about the significance of cyber security for the steady operation of systems
- Learn about cyber security concepts and OSI security architecture
- Research and identify examples of passive and active cyber-attacks and discuss their challenges
- Install Kali Linux and practise using basic commands.


## 1.1.0 Activity: Exploring cyber security concepts

Approx. 3 hours to complete all tasks in this activity

In this first activity you’ll explore some of the key concepts in cyber security. You’ll start by 
watching a video of cyber security professionals discussing the field of cyber security. You’ll then 
read about the CIA triad and check your understanding before applying it to an example company asset.

The concepts explored in this activity will give you foundational knowledge in this subject and provide
some context for all your assessments and future weeks of learning. This content will be assessed 
directly as part of your exam in Assessment 3.


### 1.1.1 Learn from cyber security professionals

Approx. 45 minutes to complete this task

#### Watching interviews with cyber security professionals

In this task you’ll watch interviews with cyber security professionals. These interviews should provide 
some insight into what you might be doing in the near future and give you some inspiration going forward.

The internet continues to grow, with more businesses using it to extend their global reach and more people 
relying on the flexibility of the internet for education, shopping, banking and work. The increased use 
of the internet also creates more opportunities for cybercriminals, as it increases the attack surface area.

The cyber security field uses diverse expertise in programming, risk analysis, system design, and tools 
to investigate crime and business processes. The cyber security field provides a wide range of career 
opportunities, from entry level to expert level. A dynamic environment, there are new challenges to address 
every day, so there will never be a dull moment in the cyber professional’s life.

#### Watch the video

"The cyber security field today" (4:44 min)

Watch the video below in which cyber security professionals discuss the field of cyber security, its 
importance to business and how it operates in business today.

As you watch, keep the following questions in mind.

- Why is cyber security important in business today?

    ```text
    Cyber security is important in business today because of the increased use of the internet, which creates more opportunities for cybercriminals. It is essential for protecting sensitive information, maintaining customer trust, and ensuring the smooth operation of business processes.
    ```
- What is risk-based security?

    ```text
    Risk-based security is an approach to cyber security that focuses on identifying and prioritizing risks to an organization's assets and implementing security measures based on the level of risk. It involves assessing the potential impact of threats and vulnerabilities and allocating resources to mitigate those risks effectively.
    ```
- Which job opportunities in cyber security most excite you?

    ```text
    There are no job opportunities in Cyber Security! Companys will avoid hiring cyber security professionals because companies don't want to spend money on cyber security. If a company has a cyber attack, they can just pay the ransom and move on with their business.
    ```


### 1.1.2 Explore cyber security concepts

Approx. 1 hour to complete this task


#### Reading about key concepts in cyber security

In this task you’ll read about key concepts in cyber security. This will give you a broad foundational 
knowledge of the concepts explored in this course.

Three basic computer security concepts play an important role in determining the cyber protection 
needed for a system:

- **Confidentiality**
- **Integrity**
- **Availability**

Collectively, they are known as the CIA triad. It is impossible to provide absolute solutions to systems, 
so CIA concepts can be used to gauge the level of risk-based security for a given system.

Read - The following reading introduces you to CIA and the cyber protection needed for a system.

> Read pages 18-24 (Chapter 1) of: Network security essentials: applications and standards (Stallings 2017)Links to an external site.

As you read, consider the following:

- #### What are some examples of confidentiality, integrity and availability?

   - **Confidentiality**: student grade information should only be accessible to students, parents, and 
   authorized staff. The chapter also notes that enrollment information may have a moderate confidentiality 
   level, while public directory information may have a low confidentiality level.

   - **Integrity**: a hospital patient’s allergy information must be correct and up to date. If someone 
    alters it, the result could seriously harm a patient, so this is a high-integrity example.

   - **Availability**: a system that provides authentication services for critical systems must remain 
   available. If it goes down, staff and customers may be unable to access essential services. The chapter 
   contrasts this with a university public website, which is important but usually only moderate in 
   availability needs, and an online phone directory, which has relatively low availability requirements.


- #### Are these three aspects always equally important to a company?

    So, Are they always equally important?

    - No. The chapter makes it clear that confidentiality, integrity, and availability are not always equally important to a company.
    - Their importance depends on the type of asset and the impact if that aspect is lost.
    - For example:
      - Confidentiality is especially important for private records such as student grades.
      - Integrity is especially important for medical data such as patient allergy records.
      - Availability is especially important for critical authentication or access systems.

The conclusion is that companies don't treat all three aspects equally in every case. They assign 
different impact levels, such as low, moderate, or high, depending on the business function, legal
obligations, safety risks, and operational consequences.


### 1.1.3 Evaluate key concepts in cyber security

Approx. 30 minutes to complete this task

#### Applying your understanding of the CIA triad

In Task 1.1.2 you read about the CIA triad. In this task you’ll check your understanding of the three 
key features of this model by looking at examples of each.

Review the three aspects of the CIA triad.

**Confidentiality:** => Preventing unauthorised people from accessing information.

**Integrity:** => Ensuring that information is not altered by unauthorised people.

**Availability:** => Ensuring that information is available to authorised people when they need it.


#### Check your understanding of the CIA triad

Complete the task below to check your understanding of the CIA triad.

Match each example to one of the three areas of the CIA triad:

- Confidentiality
- Integrity
- Availability.

The examples are:

1. The number of items on a physical shelf matches the number of items in the database => **Integrity:**
2. Only certain people have access to payroll database => **Confidentiality:**
3. Customers are able to withdraw money from their bank accounts when they need to => **Availability:**
4. Unauthorised users are not allowed to access customers personal information => **Confidentiality:**
5. Customers have confidence that their bank account balance is correct => **Integrity:**
6. A computer system continues to operate after an interruption to the power supply => **Availability:**
7. A company’s website is available to customers 24/7 => **Availability:**
8. A company’s website is unavailable to customers for a day due to a cyber-attack => **Availability:**
9. A company’s website is unavailable to customers for a day due to a power failure => **Availability:**

Although all three aspects offer full protection to a company, depending on the business, one aspect 
may be more important than another and have a higher impact level. Read the following scenarios and 
consider which may have the highest impact level and why.

Which aspect may have the highest impact level for a social media company (e.g., Facebook) in terms of CIA triad?

- Confidentiality? or
- Integrity? or
- Availability?

> Answer: Confidentiality => Users want to keep their information private

Which aspect may have the highest impact level for a bank in terms of CIA triad?

- Confidentiality? or
- Integrity? or
- Availability?

> Answer: Integrity => Customers want to be sure that their information is not altered by unauthorised people

Which aspect may have the highest impact level for a hospital in terms of CIA triad?

- Confidentiality? or
- Integrity? or
- Availability?

> Answer: Confidentiality => Patients want to keep their medical information private


### 1.1.4 Discuss key concepts in cyber security

Approx. 45 minutes to complete this task


#### Applying your knowledge to an example company asset

Now that you have examined the aspects of the CIA triad in more detail, you’ll apply your understanding
to an example company asset and discuss your findings with your peers to consolidate your understanding.

Discuss - Complete the following task:

> Note that, I don't give a monkeys about other people's opinions on this topic!

- Choose one of the assets of a company below (A or B).
- Identify examples of each aspect of the CIA triad:
  - confidentiality
  - availability
  - integrity.
- Assign a low, moderate or high impact level for the loss of each aspect.

Share your ideas on the discussion board. Be sure to include a justification of your answers.

Locate and read at least two posts by peers who chose the same asset as you.

- Compare your ideas. Did you agree?
- Comment on any factors that might have been missed.

##### Example A
An information system used for large acquisitions in a contracting organisation contains both sensitive, 
pre-solicitation phase contract information and routine administrative information. Assess the impact for 
the two data sets separately and the information system as a whole.

##### Example B
The examinations department of a university electronically stores details related to examination particulars
(e.g., question papers of forthcoming examinations, grades obtained and examiner details). The university’s 
administrative department electronically stores the students’ attendance particulars and internal assessment 
results. Assess the impact for the two data sets separately and the information system as a whole.

Source: Adapted from Problem 1.4 in Network security essentials: applications and standards (Stallings 2017), page 43.


## 1.2.0 Activity: Examining security architecture and security attacks

Approx. 3 hours 30 minutes to complete all tasks in this activity

In **Activity 1.1** we looked at the CIA triad and the fundamentals of cyber security. In this activity 
you’ll explore key areas of **Open Systems Interconnection (OSI) architecture**, including security attacks, 
security mechanisms and security services.

You’ll conduct some research on passive and active attacks and discuss the challenges in both detecting 
and preventing them. Finally, you’ll reflect on your learning in this course so far. This will continue 
to build your foundational knowledge in the field of cyber security.

### 1.2.1 Examine security architecture and security attacks

Approx. 1 hour to complete this task

#### Reading about security architecture and security attacks

In this task you’ll continue reading about key areas of cyber security, including security architecture 
and security attacks. This will support your understanding of your tasks in all assessments.

Open Systems Interconnection (OSI) architecture provides flexible approaches in understanding the security 
needs of a system and then systematically determining the required security services to safeguard the system. 
The OSI model can help when choosing risk-mitigation strategies for the resources of an organisation.

Read - The following reading provides information on security attacks, mechanisms and services.

> Read pages 24-32 (Chapter 1) of: Network security essentials: applications and standards (Stallings 2017).

As you read, consider the following:

- #### What are some examples of security architecture, security attacks, security mechanisms and security services?

    - Security architecture:
        - The chapter uses the OSI security architecture, specifically ITU-T X.800, as a systematic framework for 
        organizing security requirements and the approaches used to satisfy them.
        - It focuses on three main elements: security attacks, security mechanisms, and security services.
    - Security attacks:
        - Passive attacks:
            - Release of message contents => Eavesdropping
            - Traffic analysis => Monitoring communication patterns
        - Active attacks:
            - Masquerade => Impersonating another user or system
            - Replay => Reusing valid data transmission maliciously
            - Modification of messages => Altering message contents
            - Denial of service (DoS) => Disrupting service availability
    - Security mechanisms:
        - Encipherment => Encryption
        - Digital signature => Verifying authenticity and integrity
        - Access control => Restricting access to resources
        - Data integrity mechanisms => Ensuring data has not been altered
        - Authentication exchange => Verifying identities
        - Traffic padding => Obscuring traffic patterns
        - Routing control => Managing data paths
        - Notarization => Providing proof of actions
        - Pervasive mechanisms such as trusted functionality, security labels, event detection, security audit trails, and security recovery
    - Security services:
        - Authentication => Verifying identities
        - Peer entity authentication => Verifying the identity of a peer entity
        - Data-origin authentication => Verifying the origin of data
        - Access control => Restricting access to resources
        - Data confidentiality => Ensuring data is not disclosed to unauthorized entities
        - Connection confidentiality => Ensuring the confidentiality of a connection
        - Connectionless confidentiality => Ensuring the confidentiality of individual messages
        - Selective-field confidentiality => Ensuring the confidentiality of specific fields within a message
        - Traffic-flow confidentiality => Ensuring the confidentiality of traffic patterns
        - Data integrity => Ensuring data has not been altered
        - Connection integrity with recovery => Ensuring the integrity of a connection with recovery
        - Connection integrity without recovery => Ensuring the integrity of a connection without recovery
        - Selective-field connection integrity => Ensuring the integrity of specific fields within a connection
        - Connectionless integrity => Ensuring the integrity of individual messages
        - Selective-field connectionless integrity => Ensuring the integrity of specific fields within individual messages
        - Nonrepudiation
            - Nonrepudiation of origin => Ensuring the origin of data cannot be denied
            - Nonrepudiation of destination => Ensuring the destination of data cannot be denied
        - Availability service => Ensuring the availability of resources


- #### What are the differences between security threats and attacks?

    - A threat is a potential for a security violation. It is a possible danger that could exploit a vulnerability 
      and cause harm.
    - An attack is an actual deliberate attempt to violate security. The chapter describes it as an assault on 
      system security that comes from an intelligent threat.
    - In short:
        - Threat = possible danger
        - Attack = deliberate action taken to exploit that danger

- #### What are the differences between passive and active attacks?

    - Passive attacks:
        - Aim to learn or observe information without changing the system or data
        - Examples:
            - Reading message contents
            - Studying communication patterns through traffic analysis
        - Key characteristic:
            - Difficult to detect, because no data is altered and the system appears to operate normally
        - Main defense:
            - Prevention, usually through encryption
    - Active attacks:
        - Aim to alter data, inject false data, impersonate someone, or disrupt operations
        - Examples:
            - Masquerade
            - Replay
            - Message modification
            - Denial of service
        - Key characteristic:
            - Harder to prevent completely, because there are many possible vulnerabilities
        - Main defense:
            - Detection and recovery, rather than perfect prevention
        - Key characteristic:
            - Harder to prevent completely, because there are many possible vulnerabilities
        - Main defense:
            - Detection and recovery, rather than perfect prevention

_The OSI security architecture in X.800 is a framework for understanding security in terms of attacks, 
mechanisms, and services.  Examples of attacks include passive attacks such as release of message contents 
and traffic analysis, and active attacks such as masquerade, replay, message modification, and denial 
of service (DoS).  Examples of mechanisms include encipherment, digital signatures, authentication exchange,
and security audit trails. Examples of services include authentication, access control, confidentiality, 
integrity, nonrepudiation, and availability. A threat is a possible danger that may exploit a vulnerability, 
while an attack is the deliberate action taken to violate security. Passive attacks try to observe 
information without changing it and are hard to detect, whereas active attacks try to alter or disrupt 
systems and are harder to prevent completely._


### 1.2.2 Research examples of attacks (DISCUSSION)

Approx. 45 minutes to complete this task

#### Researching types of security attacks

In Task 1.2.1 you read about passive and active security attacks. In this task, you’ll research, 
identify and share a real-life example of a cyber-attack. This will help you to relate course 
subject materials to real-world problems.

#### Research
Identify and examine a real-life example of either a passive or an active cyber-attack by doing research online.

#### Discuss

Share your ideas on the discussion board. Be sure to include:

a summary of the cyber-attack and a link to the article/website
whether the attack was passive or active and a justification of your answer.
Read at least two posts by your peers.

Are there any similarities between your attacks?
Note: you’ll use this in Task 1.2.3.


### 1.2.3 Compare types of attacks

Approx. 45 minutes to complete this task


#### The challenges of cyber-attacks

In Task 1.2.2, you researched examples of passive and active cyber-attacks. In this task you’ll 
review the examples, compare and contrast the types of attacks, and discuss each type’s particular 
challenges.


#### Discuss

Passive and active attacks each come with their own unique challenges. Review the posts made by 
your peers in Task 1.2.2. Think about the difference between these two types of attacks.

Write a post comparing the different types of attacks. Consider the following:

- How are the attack types the same? How are they different?
- Which type is more difficult to find? Which type is more difficult to prevent?


### 1.2.4 Reflect on cyber security (REFECTION)

Approx. 1 hour to complete this task

#### Reflecting on your relationship to cyber security

In this task you’ll reflect on your learning in this course so far. This will help you to consolidate 
your foundational understanding for this course.


#### Reflect

> Too much reflection => Don't think, just do!

As a university student, and later as a cyber security professional, it’s important to develop reflective 
skills as this leads to more critical thinking.

Throughout this course, you’ll be asked to reflect on your understanding and experience. You should use 
a dedicated journal for these reflections, which may be either a physical notebook or an online resource. 
Your notes are private and you won’t need to submit them, but they’ll be useful to refer to as you develop 
your computer skills and complete your assessments.

This week has laid the foundation for learning in this course.

Think back to your readings and discussions so far this week. Write a reflection in your journal.

You may wish to answer the following questions in your reflection:

- What information did you know already? What has been most interesting/surprising?
- What do you think are your biggest responsibilities as a cyber security professional?
- How could the OSI security model help you as a cyber security professional?

---

END OF WEEK 1 MODULE => Move on to Week 1-2 Lab/Workshop