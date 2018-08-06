# xDAC Functional Specification

## Introduction

Purpose of this document

This document is the definitive specification of xDAC core and xDAC company functionalities to be developed under the xDAC Project. It is a primary input to the technical development of those facilities and the primary specification of the criteria against which the acceptability of those facilities will be evaluated after they have been developed.  

This document is intended to be read by:

a.	all responsible for the management of the developments in question, including participants in the xDAC Project

b.	business owners, customers, team members, and other interested parties in xDAC Project and Platform

c.	contractors who undertake all or parts of the development, as optional illumination of the source of and background to the specific requirements to which they are working. 

# xDAC Platform dApp (Alpha)

Alpha version of the xDAC platform will provide access to the homepage with a list of existing xDAC companies, registration of the new xDAC company, token sale and public profile (dashboard) of the xDAC company.

## Flowchart

![xDAC dApp flowchart Flowchart](/images/xDAC-dApp-flowchart.jpg)

# 1. Home Page

The xDAC homepage provides easy access to existing xDAC companies through the list in form of tiles and "search" option. Search option searches in core database by company name, token symbol or company account name. The homepage offers filtering companies by token sale status (Active or Completed) or by company industry.

The header of the page holds button "Start new company". Button "Buy XDAC" is placed in the footer of the page along with social media links and links to About and ICO pages or xDAC network tracker and wallet.

![xDAC dApp flowchart Flowchart](/images/xDAC-homepage.jpg)

# 2. Company Registration (PR-0100)

## 2.1.	Architecture

![xDAC Registration Flowchart](/images/xDAC_register-comp-flowchart-v1.07.jpg)

## 2.2.	Company Registration Form (Step 1)

The user sends a request to register a new company. Registration form contains: 

Column | Datatype | Size | Description
----|----|----|----|
c_name | std::string | 30 | Company name
c_aname | account_name | 12 | Company account name
p_aname | account_name | 12 | Personal account name
c_industry | uint32_t | 10 | Industry type
t_name | std::string | 20 | Token name
t_symbol | symbol_type | 8 | Token symbol
t_tsuply | asset | 8 | Total supply
t_isupply | asset | 8 | Initial supply
t_price | double | 10 | Token price  (min 0.001 XDAC) 
t_lockup_period_days | uint32_t | 4 | Lock-up period (max 9,999 days) 

*	Required intial capital (t_isupply * t_price)

**Industry types:**
<option value="art">Art</option>
<option value="artificial-intelligence">Artificial Intelligence</option>
<option value="banking">Banking</option>
<option value="big-data">Big Data</option>
<option value="business-services">Business services</option>
<option value="casino-gambling">Casino &amp; Gambling</option>
<option value="charity">Charity</option>
<option value="communication">Communication</option>
<option value="cryptocurrency">Cryptocurrency</option>
<option value="education">Education</option>
<option value="electronics">Electronics</option>
<option value="energy">Energy</option>
<option value="entertainment">Entertainment</option>
<option value="health">Health</option>
<option value="infrastructure">Infrastructure</option>
<option value="internet">Internet</option>
<option value="investment">Investment</option>
<option value="legal">Legal</option>
<option value="manufacturing">Manufacturing</option>
<option value="media">Media</option>
<option value="other">Other</option>
<option value="platform">Platform</option>
<option value="real-estate">Real estate</option>
<option value="retail">Retail</option>
<option value="smart-contract">Smart Contract</option>
<option value="software">Software</option>
<option value="sports">Sports</option>
<option value="tourism">Tourism</option>
<option value="virtual-reality">Virtual Reality</option>

The minimum amount of required capital is 100 XDAC, therefore initial supply or token price must be set the way so require capital reaches at least 100 XDAC.

![xDAC Registration form](/images/xDAC-Company-registration-form.jpg)

## 2.3.	Create New Personal Account (Step 2)

If the user doesn’t have a personal account yet, it can be created in sidebar form and deployed to the network free of charge. Sidebar form contains  

*	Account name (12 [a-z12345.])
*	Full user name
*	Owner private key (option to generate)
*	Active public key (option to generate)

xDAC needs to be an owner of the account due to the further function of that will be added to team members and platform participants. xDAC is the owner *, user permission is active.

*\* While  system is in development xDAC reserves the right to manage company contracts to develop all functionalities. Owner will be removed after all company segments are deployed.*

![xDAC New Personal Account](/images/xDAC-new-personal-account.jpg)

![xDAC New Personal Account Done](/images/xDAC-new-personal-account-done.jpg)

## 2.4.	Data Verification (Step 3)

The request is sent to core contract and checked for valid data and duplicates. All form field must be filled out. Company name, company account name and token symbol must be unique. If duplicates are found, we will display “whois” option to locate an existing company with identical data. Whois link will open related company dashboard in new tab. Initial supply should not exceed total supply. 

![xDAC Registration form error](/images/xDAC-Company-registration-form-error.jpg) 

## 2.5.	Buy Equity in New Company (Step 4)

After data validation, Register Company button will open the Buy Equity sidebar. The sidebar contains a form with:

*	Equity in XDAC coins
*	Equity in percent

Data are correlated. If one is changed, other changes accordingly. After specifying the amount, the user can buy equity via Scatter. 

![xDAC Buy Equity Tokens](/images/xDAC-buy-equity.jpg) 

## 2.6.	Company Submission & Core Contract (Step 5)

Proceeds from equity purchase are transferred to the core contract with all submitted data. 

Core contract is a bridge between company registration dApp and a company account. It holds the investments until the company is created and deployed to the network. Furthermore, the core contract manages and stores data in the central database of companies. The central database stores the following data:

Table ***token***

Column | Datatype | Size | Description
----|----|----|----|
t_name | std::string | 20 | Token name (max 20 chars)
t_tsuply | asset | 10 | Total supply (min 1)
t_isupply | asset | 10 | Initial supply (min 1)
t_price | double | 10 | Token price (min 0.001 XDAC)
t_symbol | symbol_type | 8 | Token symbol (max 8 Chars) 
t_gained_xdacs | asset | 8 | The sum of received investments in XDAC
t_lockup_period_days | uint32_t | 4 | Lock-up period (max 9,999 days) 

Table ***settings***

Column | Datatype | Size | Description
----|----|----|----|
c_aname | account_name | 12 | Company account name
c_founder | account_name | 12 | Company founder
c_createdts | uint64_t | 20 | Company creation timestamp
c_deployed | bool | 1 | Company account creation
c_contract | bool | 1 | Company contract deployed
c_locked | bool | 1 | Company is live or frozen
c_rating | uint32_t | 10 | Company performance rating

Table ***meta***

Column | Datatype | Size | Description
----|----|----|----|
c_name | std::string | 30 | Company name (max 30 chars)
c_desc | std::string | 1000 | Company description
c_tag | std::string | 250 | Company short description (max 250 chars)
c_media | std::string | 256 | Link to company media
c_contact | std::string | 50 | Company contact email

Table ***lfund***

Column | Datatype | Size | Description
----|----|----|----|
c_lfrate | double | 0.00 | Company liability discount rate
c_lfcap | double | 10 | Cap of company libility fund 
c_lfbalance | double | 10 | Balance of company liability fund 

Table ***investors***

Column | Datatype | Size | Description
----|----|----|----|
i_pk | uint64_t | 20 | Investor public key
i_caname | account_name | 12 | Company account name
i_paname | account_name | 12 | Investor personal account name
i_quantity | asset | 10 | Number of tokens investor holds
i_tokens | asset | 10 | 
i_issued | bool | 1 | Token issued TRUE or FALSE

Table ***investmenttx***

Column | Datatype | Size | Description
----|----|----|----|
itx_pk | uint64_t | 20 | Investment tx public key
itx_caname | account_name | 12 | Investment tx company account name
itx_paname | account_name | 12 | Investment tx personal account name
itx_quantity | asset | 10 |
itx_tokens | asset | 10 | 

Table ***investmentvotes***

Column | Datatype | Size | Description
----|----|----|----|
iv_pk | uint64_t | 20 | 
itx_pk | uint64_t | 12 | 
i_pk | uint64_t | 12 | 
iv_caname | account_name | 10 |
iv_paname | account_name | 10 | 
iv_approve | bool | 1 | 

## 2.7.	Deploying Company (Step 6)

Core contract is responsible for deploying company through nodejs service to xDAC network while investment remains on core contract. Deploying process has the following steps:

### 2.7.1.	Deploying company account

A new multi-sig account on the xDAC network is created with xDAC as the only owner. Permissions of created account are: 
* xDAC (***owner***) weight 1, threshold 1 (will be removed after platform development),
* Founder (***active***) weight < stake in the company >, threshold 51, 
* Founder (***publish***) weight 1, treshold 1.

**Permissions**

***owner*** authority symbolizes right to administrate the account. Deploy or update existing smart contracts and features. Throughout development, only xDAC delegates will have full authority to manage the company account. After development, only block producers with the consent of the network users can release updates that affect company accounts.

***active*** authority is used for transferring funds above the threshold, voting for company executives, approving company actions, voting for producers and making other high-level account changes.

***publish*** authority is used for making other low-level updates, transferring funds below the threshold, hiring team members or resolving disputes. 

### 2.7.2.	Creating company contract

Smart contract manages the transfer of funds between company account and liability fund. All received transactions must be distributed between the liability fund and company account based on the liability fund discount rate until the liability fund cap is reached.

### 2.7.3.	Creating company database

Storage contract is database storing company information and records. At company creation database has following tables:

Table ***cusers***

Column | Datatype | Size | Description
----|----|----|----|
cu_paname | account_name | 12 | Company member personal account name
cu_role | std::string | 1 | O (owner - founder, investor or owner) or M (member - team member or advisor)
cu_supervisor | account_name | 12 | Team member supervisor
cu_fname | std::string | 20 | Member first name
cu_lname | std::string | 20 | Member last name

Initial record is:

cu_paname | cu_role | cu_fname | cu_lname
----|----|----|----|
< Founder personal account name > | O | empty | empty

Table ***cmeta***

Column | Datatype | Size | Description
----|----|----|----|
c_aname | account_name | 12 | Company account name
c_name | std::string | 30 | Company name (max 30 chars)
c_industry | uint32_t | 10 | Industry type
c_desc | std::string | 1000 | Company description
c_tag | std::string | 20 | Company short description (max 250 chars)
c_logo | std::string | 0 | 

Initial records are:

c_aname | c_name | c_industry | c_desc | c_tag | c_contact | c_logo | c_pimg
----|----|----|----|----|----|----|----|
< Company account name > | < Company name > | < Industry type > | empty | empty | empty | empty

Table ***cmedia***

Column | Datatype | Size | Description
----|----|----|----|
c_aname | account_name | 12 | Company account name
c_type | std::string | 30 | Media type
c_media | std::string | 256 | Media link
c_mpublished | uint64_t | 20 | Published timestamp 

Media types:
* Whitepaper
* Onepager
* Video
* Facebook
* Twitter
* Reddit
* Github
* Email
* URL
* Telegram
* Bitcointalk

Table ***c_contracts***
* contract_id
* contract_name
* contract_ver
* contract_rdate

Initial record are:

contract_id | contract_name | contract_ver | contract_rdate
--- | ----------- | ----- | --------
1 | company contract | 1.0.0 | < Unix Timestamp >
2 | storage contract | 1.0.0 | < Unix Timestamp >
3 | lf contract | 1.0.0 | < Unix Timestamp >

Each company smart contracts must have a name and a version number stored in ***company_contracts*** table. Other smart contracts or dApps will interact with storage contract before each call. Storage contract will return name and version number of the most recent contract.

### 2.7.4. Equity Tokens Issuance

Deploy equity token contract with parameters specified by the company founder. If the initial supply is less than the total supply, only the amount of initial token supply is issued. Remaining tokens can be issued by company owners in the later stage.
In case tokens have a lock-up period, tokens should not be transferable until lock up period expires.

<!-- ### 1.7.5. Liability Fund Contract

Liability fund is collateral in the form of smart contact holding XDAC tokens in case of the company debts or liabilities.
Funds on liability fund during company existence can be accessed only by dispute representative board. In upcoming updates company owners will be able to increase or decrease the liability fund discount rate or cap.

After a company is acquired, liquidated, or closed, a Liability Fund will be distributed between owners based on their respective stake in the company.-->

# 3. Equity Tokens Sale (PR-1800) (Step 7) 

## 3.1. Buy Equity Tokens

Anyone who has access to the Token Sale page can join equity token sale by submitting an offer to purchase tokens. Offer can be submitted in any amount and company o Following situations can arise:

### 3.1.1. Investor doesn’t have Scatter

After clicking on Buy button Create Personal Account in the sidebar is opened. After creating an account we will prompt the user to download Scatter.

### 3.1.2. Investor doesn’t have xDAC personal account

After click on Buy button Create Personal Account in the sidebar is opened.

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-personal-account.jpg)

### 3.1.3.	Investor doesn’t have XDAC coins

Buy XDAC Coins in the sidebar is opened. 

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-buy-xdac.jpg)

### 3.1.4.	Investor has ERC20 XDAC tokens

Swap XDAC tokens for XDAC coins in the sidebar is opened.  

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-swap.jpg)

### 3.1.5.	Investor submitting offer

After the company sold 51% of equity tokens, all new investments are submitted in form of offer and owners can decide to accept or decline the offer. The offer must be equal to or greater than the amount of nominal token value.
The offered amount is transferred to the company core contract. Approval of investment transfers funds to the company. Declined offers are refunded back to the investor.  

![xDAC Buy Equity Tokens](/images/xDAC-Token-Sale-buy-offer.jpg)

### 3.1.6.	Investor has Scatter, account and coins

After investors created a personal account and fund their account with XDAC coins, they can purchase equity in the company.

## 3.2.	Token Sale (Step 8)

Company Token Sale is company crowdfunding option to raise funds from different investors or partners. Token sale page holds company summary information and a list of existing token holders. Anyone can access this page at xdac.co/s/< company account name > and purchase equity through Buy Equity Tokens button. This page can be shared with others via email.

Following situations can arise during the token sale:

### 3.2.1.	Company token sale 

The company disposition of tokens is available until all equity tokens are sold. Unsold equity tokens are available to public investors or partners.

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-50p.jpg)

### 3.2.2.	Company owned by single owner

If the company sold 100% of initial supply to single owner, Buy Equity Tokens option is no longer available. This round of token sale is completed. 

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-100p.jpg) 

### 3.2.3.	51% of equity tokens owned by one account

If the company is controlled by a single account, the account owner has the authority to approve all new investment offers.

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-60p.jpg) 

After the company sold 51% of equity tokens, all new investments are submitted in form of offer and owners can decide to accept or decline the offer. The offer must be equal to or greater than the amount of nominal token value.
The offered amount is transferred to the company core contract. Approval of investment transfers funds to the company. Declined offers are refunded back to the investor.  

![xDAC Buy Equity Tokens](/images/xDAC-Token-Sale-buy-offer.jpg)

### 3.2.4.	51% of equity tokens owned by multiple accounts

Investments up to 51% are accepted without approval and in nominal value. As soon as the amount of sold equity tokens reaches 51% or more, authorization of new investment offers is required by the owners holding at least 51%.

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-60p-3.jpg)

Each investment received after reaching 51% will be separated in the list by a different color and marked with three dots (“…”) representing pending status. Pending status is visible to the public. Owners with installed Scatter can see arrow option which let them vote on accepting or declining the investment.

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-40p-approval.jpg)

If the investment is approved by the owner with 40% stake, approval percentage will increase to 40% and the account will not be able to approve investment again. However, the same account can decline investment and reset approval.

Progress bar below investment offer shows voting status for owners to see which transactions still need voting.

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-40p-approved.jpg)

After investment approval reaches 51% of votes or more, investment is accepted and transferred from a core contract to company contract which distributes investment between account and liability fund.

Declined investments by 51% of votes or more will be refunded from core contract back to account of the investor.

### 3.2.4.	Buy offer canceled by investor

An investor can decide to cancel own offer at any time. Offer is automatically removed from the list and refunded back to investor account.

![xDAC Equity Tokens Sale](/images/xDAC-Token-Sale-cancel-offer.jpg)

### 3.2.5.	Company has unsold tokens

If the company sold more than 51% of equity tokens, owners can decide to terminate token sale and distribute remaining tokens proportionally to investors. This means that if an investor has bought 1% of company equity tokens, he/she will receive 1% of the unsold tokens. This option will be available from company dashboard.

## 3.3.	Release of funds (Step 9)

After company contracts are deployed, nodejs will notify xDAC core and core contract will release equity funds to company contract and liability fund.

# 4. Company Dashboard - Public Profile (PR-0300) (Step 10)

Public company profile accessible through link xdac.co/<account name>. Edit of public profile accessible with help of Scatter for permission Active.

![xDAC Company Dashboard](/images/xDAC-company-dashboard.jpg)

Edit option opens a form for editing company logo, tag, description of media links.   

![xDAC Company Dashboard Edit Story](/images/xDAC-company-dashboard-edit.jpg)