# xDAC Requirements Document

# 1 Introduction

This document is the definitive specification of the user requirements for xDAC companies to be developed under the xDAC Project.  It is a primary input to the technical development of those facilities, and the primary specification of the criteria against which the acceptability of those facilities will be evaluated after they have been developed.  

This document is intended to be read by:

a.	all responsible for the management of the developments in question, including participants in the xDAC Project

b.	business owners, customers, team members, and other interested parties in xDAC Project and Platform

c.	contractors who undertake all or parts of the development, as optional illumination of the source of and background to the specific requirements to which they are working. 


**Reference Documents**

Ref | Document ID | Title | Revision
--- | ----------- | ----- | --------
RD1 | WP001|xDAC Whitepaper| 1.0.8

**Definitions, Acronyms and Abbreviations**

Tag | Description
--- | -----------
AA | Autonomous Agent (Bot, robot, AI, smart applications)
DAC| Decentralized autonomous company
DRB | Dispute Representative Board
Initial Capital | The initial capital is amount of XDAC to start company and distribute company ownership among owners. The minimum amount of initial capital is 100 XDAC. 1 XDAC is one vote in the company. If company has multiple partners, they can participate in the company by sending XDAC tokens from a different wallet addresses in an amount that represents their stake.
Performance Rating | It is a mechanism that allows for an automated rating based on tracking work ethic and delivering tasks on time. Each task will be rated between 0 and 1 (0 means task not finished, not delivered, or not paid on time) whereas (1 means task was finished and payment initiated). 
PR | Product Requirements
RD | Requirements Document
UN | User Needs
UR | User Requirements
XDAC | Platform Currency. XDAC will be used for: company creation, merchant payments, pay team members (payrolls), liability fund, dispute resolutions, profit distribution.
xDAC Company| xDAC is a DAC created and operated on xDAC Platform by one or multiple human or autonomous agent owners or a mixture of both that share a common purpose and unites in order to achieve specific, declared goals.
xDAC Liability Fund | An xDAC Liability Fund is coverage in case the xDAC's debts or liabilities exceed a certain debt-to-equity ratio. It is calculated as a percentage of received payments stored in a separate wallet until certain threshold is reached. Liability fund is not accessible to owners during the company's existence and is available for transfer 90 days after the company is ceased or transferred to new owner. 
xDAC Platform | An xDAC platform takes full advantage of decentralized ledger technology and lets anyone create and manage a company without the limitations of geography.

# 2 User Needs and User Requirements

## 2.1 User Needs

Entrepreneurs and business owners need a platform which can help them create an automated company fast and easy, independent from banks and jurisdictions and free from 3rd party influencers so owners can be in control of company processes, data, and finances.


## 2.2 User Needs Description

UN ID | User Need | Source
----- | --------- | ------
UN-0100 | Fast and simple company registration and management with automated governance, free from jurisdiction limitations | Group A
UN-0200 | Company free from financial institutions | Group A
UN-0300 | Automated dispute resolution | Group A
UN-0400 | Simple team management tools | Group A
UN-0500 | Simple project management tools | Group A
UN-0600 | Simple fundraising tools | Group A
UN-0700 | Owners vote on proposals | Group A

## 2.3 User Requirements

UR ID | UN ID | User Requirement  | Description
----- | ----- | ----------------- | -----------
UR-0100 | UN-0100 | Company via browser | Register company via a web browser or dApp from computer or smartphone 
UR-0200 | UN-0100 | Company profile | Public company profile with company details that combines business registry, certificate of good standing, ICO listing, LinkedIn company profile and company rating
UR-0300 | UN-0100 | Company Bylaws | Bylaws in digital form regulated by smart contract
UR-0400 | UN-0100 | Company Assets | List of company assets
UR-0500 | UN-0100 | Partners | List of partners in company with an option to add or remove partners
UR-0600 | UN-0100 | Ownership Transfer | Option to transfer company to a new owner
UR-0700 | UN-0200 | Company Wallet | Company cryptocurrency wallet to send or receive payments
UR-0800 | UN-0200 | Transactions | Company wallet transaction history
UR-0900 | UN-0200 | Mechant Tools | Buy Now button and shopping cart for online purchases
UR-1000 | UN-0300 | Dispute Management | Cheap and simple dispute resolution via decentralized arbiters
UR-1100 | UN-0400 | Team Management | Manage team, their positions, and permissions
UR-1200 | UN-0400 | Automated evaluation | Evaluate automatically team members based on their performance
UR-1300 | UN-0500 | Project Management | Manage projects and tasks, assign tasks to team members and pay them automatically when the task is finished
UR-1400 | UN-0600 | Fundraising Tools | Issue new tokens and start ICO or private sale
UR-1500 | UN-0700 | Voting | Owners can submit new proposals and vote on existing platform or company proposals


# 3 Product Requirements

xDAC is a self-governed platform for creating and managing decentralized autonomous companies. The xDAC company is a public record about the entity on a distributed ledger accessible and verifiable by anyone. 

## 3.1 Product Requirements Description

PR ID | UR ID | Product Requirement  | Priority | Description
----- | ----- | -------------------- | -------- | -----------
PR-0100 | UR-0100 | Company registration | M | Company registration via a web browser. Store company name, domain, owner's email on the distributed ledger. After email verification XDAC wallet and liability fund is created. Owner and partners join the company by sending initial capital to a generated company account. The minimum amount of initial capital is 100 XDAC. Default liability fund deduction is 10%. 
PR-0200 | UR-0100 | Company Dashboard | S | Company overview with list of pending tasks, pending proposals, wallet and liability fund balances, team and company ratings.
PR-0300 | UR-0200 | Public Profile | M | Create a company public profile with a) Date of company registration, b) Amount of Initial Capital, c) Amount on Liability Fund, d) Company rating, e) List or display number of company owners, f) List or display number of team members with open position option, g) Short company tag or description (250 chars). Company owners can edit their public profile including a logo, company description or link public articles or videos.  
PR-0400 | UR-0300 | Company Bylaws | M | A form where owner(s) can define a corporation's purpose, how it will operate, and the duties and responsibilities of the owners and managers. Owners can specify ownership rights, select officers, and directors, plan meetings, and establish how to remove officers or directors. 
PR-0500 | UR-0400 | Company Assets | C | Editable list of resources or things of value that are owned by a company.
PR-0600 | UR-0500 | Partners | M | List of partners and their stakes with option to add or remove partners.
UR-0700 | UR-0600 | Ownership Transfer | S | Due diligence checklist and option to transfer company to a new owner through escrow smart contract. Liability fund released after 90 days to owners based on their stake in the company.
PR-0800 | UR-0700 | Company Wallet | M | XDAC wallet for sending and receiving payments that replaces traditional bank account.
UR-0900 | UR-0800 | Transactions | M | List of company transactions with filtering options.
PR-1000 | UR-0900 | Mechant Tools | S | Online form which lets owners generate payment buttons for their online store.
PR-1100 | UR-1000 | Dispute Management | M | Dispute management should have following options: a) start a new dispute, b) list of pending disputes, c) escalate resolved dispute, d) assign dispute to specific DRB representative, e) set price for resolving the dispute.
PR-1200 | UR-1000 | DRB Management | M | Add registration of arbiters who are representatives of decentralized DRB. Registration should create XDAC wallet for each representative. Create a pool of pending disputes where arbiters can select and resolve disputes. Representatives will be paid for dispute resolution to their XDAC wallet.
PR-1300 | UR-1100 | Team Management | S | Add option to manage a team and assign a position and permissions to each team member. UI will display a hierarchy of company structure chart. Each team member and team is rated by automated Performance Rating.
PR-1400 | UR-1100 | Hire Team Member | S | Add open position form and display open position on company public profile.
PR-1500 | UR-1100 | Open Positions | C | Create a public list of open positions where job seekers can search for open positions.


Priority: define whether the requirement is: 
- Must have (M) – must be implemented in the system.
- Should have (S) – must be implemented but may wait until a second increment.
- Could have (C) – could be implemented but it is not central to the project objectives.
- Wish to have (W) – will not be implemented but it will be considered for a future phase.





 


















