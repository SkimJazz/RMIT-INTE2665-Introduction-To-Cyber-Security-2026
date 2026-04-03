# Assessment 2: Industry-focused security report and reflection - TT1 2026

## KEY ASSESSMENT INFORMATION

- Assessment type: report/reflection
- Due date: Sunday of Week 7, 11.59pm (Melbourne time)
- Length: Report: 10–15 pages with screenshots (+/-10%); Reflection: 400 words (+/-10%)
- Weighting: 50%
- **MARK RECEIVED FOR THIS ASSESSMENT: 49/50 (98%)**

## Step 1: Get started

### Overview

During this course, you’ve learned about the architectures of firewalls and have experimented with
iptables firewalls using Kali Linux. In this assessment, you’ll utilise the tools in Kali Linux VM
to work through a set of tasks using packet filtering firewalls with iptables. You’ll follow the
detailed instructions and document your work in a report (including screenshots). After completing
the report, you’ll write a short reflection about current issues in cyber security.

You must submit:

- Part A 1 x report (10–15 pages with screenshots) .DOCX
- Part B 1 x reflection (400 words) .DOCX

## Purpose

Incidents of cybercrime are growing exponentially every year. In 2023, the Australian Cyber Security
Centre received 94,000 cybercrime reports, up 23% from the previous year (Australian Cyber Security
Hotline 2023). Firewalls are tools that can be used to regulate access to organisations’ critical
cyber assets. In this assessment, you’ll demonstrate your knowledge on firewall configurations to
ensure that the applications are accessed in an ethical, allowable manner for secure business practices.
Australian Cyber Security Hotline (2023), ASD Cyber Threat Report 2022-2023, accessed 16 October 2024.

[Cyber.gov.au](https://www.cyber.gov.au/about-us/view-all-content/reports-and-statistics/asd-cyber-threat-report-july-2022-june-2023)

## Marking criteria and rubric

**Part A**: Report (36 points) of your submission will be assessed based on the following criteria:

- Respond to prompts and complete tasks accurately (14 points)
- Describe details of task execution clearly (12 points)
- Explain key issues in the use of packet filtering firewalls (10 points).

**Part B**: Reflection (14 points) of your submission will be assessed based on the following criteria:

- Demonstrate an understanding of firewalls in cyber security (7 points).
- Communicate ideas clearly and reference appropriately (7 points).

## Step 2: Prepare

Required tools and resources for this task

Prepare by downloading/accessing the following:

- Kali Linux
- Lab manual

Assessment instructions

To complete this assessment, you’ll need to use Kali Linux (refer to Week 1 for more information if
required). Each step in Part A must be included in your report, along with screenshots documenting
your work and the results.

### Part A: Report (10–15 pages with screenshots)

#### Securing a system using a packet filtering firewall

In this part, you’ll configure and test the packet filtering firewall iptables. You should test that
the following services are installed on your machines: SSH, HTTP and MYSQL servers. Start the services
and ensure that they are available for you to complete the tasks with iptables.

1. Configure your firewall to do the following:
   - A. Reject connection on loopback interface.
   - B. Reject connection at port 22 for SSH.
   - C. Deny ping and then demonstrate that you can restore ping command functionality.
   - D. Reject all traffic coming to port 80.
   - E. Block incoming traffic connection to the IP address of your virtual machine.
   - F. Allow traffic coming to port 80 (inbound) but reject accessing a particular IP address (e.g.,8.8.8.8.).

2. Record all firewall rules and results in the report.

3. Describe in detail how you tested all configurations with real practical tests and/or with your
   gathered information in the report.

4. Management of rulesets for firewalls could become a challenge. Discuss how rulesets for iptables
   can be managed more efficiently and optimally.

5. Discuss the three attacks that can be made on the packet filtering firewalls and comment on the
   effectiveness of the counter measures for the attacks.

### Part B: Reflection

After completing the tasks in Part 1, reflect on the role of firewalls in cyber security. Consider the
following in your reflection:

- Defence in depth is a concept in cyber security where multiple security controls (physical, technical
  and administrative) are deployed to safeguard cyber systems. Reflect on the possibility that counter
  measures to firewalls attacks on technical controls may be ineffective.


## Marking  Rubric


| Criterion | Grade Band | Description | Points |
|-----------|------------|-------------|--------|
| Respond to prompts and complete tasks accurately. | HD | All tasks are fully completed. High technical skill level is demonstrated across all three areas. Task outcomes are highly accurate and precise. | 14 to >11.19 |
|  | D | All tasks are completed. Good technical skill level is demonstrated across all three areas. Task outcomes are mostly accurate. | 11.19 to >9.79 |
|  | C | Most tasks are completed. Generally good technical skill level is demonstrated across all three areas, though some areas might be less successful. Task outcomes are generally accurate. | 9.79 to >8.39 |
|  | P | All tasks are attempted, though some may be incomplete. Some technical skill level is demonstrated across two or more areas, though some areas might be less successful. At least 60% of task outcomes are accurate. | 8.39 to >6.99 |
|  | N | At least 70% of the tasks are attempted. Technical skill level is demonstrated in at least one area. At least 50% of task outcomes are accurate. | 6.99 to >0.0 |
|  | DNS | Did not submit | 0 |
| Describe details of task execution clearly. | HD | Details of task execution are described clearly, concisely and comprehensively. Report is clearly organised and easy to follow. Use of headers and screenshots is highly relevant and supports understanding. | 12 to >9.59 |
|  | D | Details of task execution are described clearly and concisely. Report is clearly organised. Use of headers and screenshots is appropriate and supports understanding. | 9.59 to >8.39 |
|  | C | Details of task execution are described clearly. Report is generally logically organised. Use of headers and screenshots is generally appropriate and supports understanding. | 8.39 to >7.19 |
|  | P | Task execution is described, though some minor details may be lacking. Report is logically organised, though may be unclear in some areas. Some use of headers and screenshots is present, though this could be used more consistently or logically. | 7.19 to >5.99 |
|  | N | Task execution is described though some key details may be lacking. May be unclear or difficult to follow. Ineffective use of headers and screenshots at times. | 5.99 to >0.0 |
|  | DNS | Did not submit | 0 |
| Explain key issues in the use of packet filtering firewalls. | HD | Discussion of key issues of packet filtering firewalls is clear, concise and comprehensive. Answers demonstrate insight. | 10 to >7.99 |
|  | D | Discussion of key issues of packet filtering firewalls is clear and concise. Answers demonstrate good understanding. | 7.99 to >6.99 |
|  | C | Discussion of key issues of packet filtering firewalls is clear. Answers demonstrate an understanding. | 6.99 to >5.99 |
|  | P | Discussion of key issues of packet filtering firewalls is present though some details may be lacking. Answers demonstrate some understanding. | 5.99 to >4.99 |
|  | N | Presents some key issues of packet filtering firewalls though information is not always clear or relevant. Answers demonstrate some basic understanding. | 4.99 to >0.0 |
|  | DNS | Did not submit | 0 |
| Demonstrate an understanding of firewalls in cyber security | HD | Demonstrates a clear, understanding of the role of firewalls in cyber security. Answers are highly relevant and demonstrate insight. | 7 to >5.59 |
|  | D | Demonstrates a clear understanding of the role of firewalls cyber security. Answers are relevant. | 5.59 to >4.89 |
|  | C | Demonstrates an understanding of the role of firewalls in cyber security. Answers are generally relevant. | 4.89 to >4.19 |
|  | P | Demonstrates some understanding of the role of firewalls in cyber security though some points may be missing. Answers are somewhat relevant. | 4.19 to >3.49 |
|  | N | Demonstrates some basic understanding of the role of firewalls in cyber security though some key points may be missing. Answers are not that relevant. | 3.49 to >0.0 |
|  | DNS | Did not submit | 0 |
| Communicate ideas clearly and reference appropriately. | HD | Consistently communicates meaning effectively through clear, unambiguous language and appropriate tone. Consistently uses appropriate, accurately positioned references; all in-text citations, references and formatting are fully to Harvard style. | 7 to >5.59 |
|  | D | Communicates meaning effectively through mostly clear, accurate language and appropriate tone. Uses mostly appropriate, accurately positioned and formatted references; in-text citations, references and formatting are to Harvard style. | 5.59 to >4.89 |
|  | C | Generally communicates clearly, though some instances of incorrect language use or tone may be evident. However, they do not obstruct meaning. Uses generally appropriate references, accurately positioned; most in-text citations, referencing and formatting are to Harvard style. | 4.89 to >4.19 |
|  | P | Generally communicates clearly, though some instances of incorrect language use may obstruct meaning at times; tone may be inappropriate. References are generally accurately formatted to Harvard style, though minor omissions may be present. | 4.19 to >3.49 |
|  | N | Communicates, though instances of incorrect language use obstruct meaning; tone may be largely inappropriate. References are positioned incorrectly or used inappropriately; major omissions in in-text citations and references are not in Harvard style. | 3.49 to >0.0 |
|  | DNS | Did not submit | 0 |

---
