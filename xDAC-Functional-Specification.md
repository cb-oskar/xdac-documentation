# xDAC Functional Specification

## Introduction

Purpose of this document

This document is the definitive specification of xDAC core and xDAC company functionalities to be developed under the xDAC Project. It is a primary input to the technical development of those facilities and the primary specification of the criteria against which the acceptability of those facilities will be evaluated after they have been developed.  

This document is intended to be read by:

a.	all responsible for the management of the developments in question, including participants in the xDAC Project

b.	business owners, customers, team members, and other interested parties in xDAC Project and Platform

c.	contractors who undertake all or parts of the development, as optional illumination of the source of and background to the specific requirements to which they are working. 

# 1.	Company Registration

## 1.1.	Architecture

![xDAC Registration Flowchart](/images/xDAC_register-comp-flowchart-v1.06.jpg)

## 1.2.	Company Registration Form (Step 1)

The user sends a request to register a new company. Registration form contains: 

*	c_name - Company name (max 30 chars)
*	c_aname - Company account name (12 [a-z12345.])
*	p_aname - Personal account name 
*	t_name - Token name (max 30 chars) 
*	t_symbol - Token symbol (max 8 Chars) 
*	t_tsuply - Total supply (max 1,000,000,000)
*	t_isupply - Initial supply (max 1,000,000,000)
*	t_price - Token price (min 0.001 XDAC) 
*	t_lockp - Lock-up period (max 9,999 days) 
*	Required capital (t_isupply * t_price)

The minimum amount of required capital is 100 XDAC, therefore initial supply or token price must be set the way so require capital reaches at least 100 XDAC.

[xDAC Registration form](/images/xDAC-Company-registration-form.jpg)

## 1.3.	Create New Personal Account (Step 2)

If the user doesn’t have a personal account yet, it can be created in sidebar form and deployed to the network free of charge. Sidebar form contains  

*	Account name (12 [a-z12345.])
*	Full user name
*	Owner private key (option to generate)
*	Active public key (option to generate)

xDAC needs to be an owner of the account due to the further function of that will be added to team members and platform participants. xDAC is the owner, user permission is active.

## 1.4.	Data Verification (Step 3)

The request is sent to core contract and checked for valid data and duplicates. All field must be filled out.  Company name, company account name and token symbol must be unique.  If duplicates are found, we will display “whois” option to locate an existing company. Initial supply should not exceed total supply. 

## 1.5.	Buy Equity (Step 4)

After data validation Register Company button will open the Buy Equity sidebar. The sidebar contains a form with:

*	Equity in XDAC coins
*	Equity in percent

Data are correlated, so if one is changed, other changes as well. After specifying the amount, the user can buy equity via Scatter. 

## 1.6.	Company Submission (Step 5)

Proceeds from equity purchase are transferred to the core contract with all submitted data. 

## 1.7.	Deploying Company (Step 6)

Data are sent to nodejs while funds remain on core contract. Nodejs will:

### 1.7.1.	Deploys company account to the network.

A new multi-sig account is created with xDAC as only owner. Company founders don’t have owner permission to the company account. At this point permissions are: xDAC (owner) weight 1, threshold 1 and founder (active) weight 1, threshold 1. (Confirm how we are going to manage owners if they constantly changing.)

### 1.7.2.	Creates company contract

Smart contract manages transfer of funds between account and liability fund. All received transactions must be divided based on liability fund discount rate until liability fund cap is reached. (confirm)

### 1.7.3.	Issue Equity Tokens
Deploy token contract with parameters specified by the founder. In case initial supply is lower than total supply, we will issue only tokens in the amount of initial supply and remaining tokens can be issued later. (confirm)
In case tokens have a lock-up period, tokens should not be transferable.   
### 1.7.4.	Creates storage contract (DB)

DB have following items:  
* c_name - Company name (editable)
* c_aname - Company account name
* c_created - Date and time of company registration
* c_tag - Company tag (60 chars) (editable) 
* c_desc - Company description (320 chars) (editable)
* c_eqprice - Equity tokens nominal value in XDAC 
* c_rating - Company rating (int 0.00, default 0)
* c_lfrate – Company liability fund discount rate (default 10%)
* c_lfcap – Company liability fund cap (default 10% of initial capital in XDAC)
* c_media – URL to public articles or media (confirm)
* c_contact - Company contact (email) (editable) 
* c_lock – Company lock (T,F) (default F)
* core_id - Core DB company ID

## 1.7.5.	Liability Fund Contract

Liability fund is smart contact which holds XDAC tokens from all received payments.
Contracts should have a version number and each contract or dApp will talk to smart contracts with highest version numbers on the accounts in case we release contract updates with the higher version number.

## 1.8.	Initial Capital Release (Step 7)

After company contracts are deployed, nodejs will notify xDAC core and core contract will release received equity funds to company contract that will divide funds between account and liability fund based on clfrate and clfcap.

## 1.9.	Token Sale (Step 8)

Company info displayed on Token Sale page with option to Buy Equity Tokens. Page also contains send page link to email address. Token sale page is on xdac.co/s/< company name >.

### 1.9.1.	Company sold 100% of equity tokens
If the company sold 100% of initial supply, Buy Equity Tokens option is no longer available.

### 1.9.2.	Company didn’t sell all equity tokens
If any remaining tokens are available, Buy Equity Tokens button is visible.

### 1.9.3.	51% owned by one account
If the company is owned by account or one account owns more than 51%, approval of all investments are done by this account only.

### 1.9.4.	51% owned by multiple accounts
Investments up to 51% do not need approval. When the amount of sold equity tokens reaches 51% or more, approval of new investments is required by owners with 51%.

Each investment over 51% will be grayed on the list of company investments with “…” – pending status (visible to public). Owners with installed Scatter can see caret with options to accept or decline transaction.

If transaction is approved by owner with 40% stake, approval percent will change to 40% and this account can’t vote again.

In case investment was declined, decline percent will change to -40%

After approval reaches 51% or more, investment is accepted and transferred from core contract to company contract which will distribute investment between account and liability fund.

If investment was declined by 51% or more, investment will refunded from core contract back to account of investor.

## 1.10.	Buy Equity Tokens (Step 9)

Anyone who has access to the Token Sale page can join equity token sale. Following situations can arise:

### 1.10.1.	User doesn’t have Scatter
After clicking on Buy button Create Personal Account in the sidebar is opened. After creating an account we will prompt the user to download Scatter.

### 1.10.2.	User doesn’t have xDAC personal account
After click on Buy button Create Personal Account in the sidebar is opened.

### 1.10.3.	User doesn’t have XDAC coins
Buy XDAC Coins in the sidebar is opened. 

### 1.10.4.	User has ERC20 XDAC tokens
Swap XDAC tokens for XDAC coins in the sidebar is opened.  

### 1.10.5.	User has Scatter, account and coins
After investors created a personal account and fund their account with XDAC coins, they can purchase equity in the company.

## 1.11.	Public Profile (Step 10)

Public company profile accessible through link xdac.co/<account name>. Edit of public profile accessible with help of Scatter for permission Active. 
