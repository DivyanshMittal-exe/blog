---
title: Printing Currency
date: 2023-06-04 12:23:00 +0530
categories: [Finance]
tags: [info, finance]     # TAG names should always be lowercase
comments: true
mermaid: true
math: true

---

Money doesn't grow on trees. However, this is because trees cannot keep up with the printing press!

## The scam of the modern banking system

Below, I describe the steps our modern banking system and governments take to infuse the system with currency that the RBI prints, and how this process erodes our wealth.

### Step 1: Deficit Spending

The government intends to spend more money than it currently brings in. This disparity is referred to as deficit spending. However, where does all the surplus currency originate?

It just asks the RBI to print more of it!

The government of India, issues bonds, treasury bills and other government securities, which the large banks bid on to buy these from the government. The bonds and bills are nothing more than a promise to repay the amount the banks have loaned the government with interest.

### Step 2: Open Market Operations
RBI then conducts open market operations in order to trade these bonds on the open market. It purchases these bonds from the banks at a premium. To cover these costs, the RBI simply prints more currency! The bank's profit can now be used to purchase additional bonds, and the cycle continues.

In anticipation of a recession caused by the COVID-19 pandemic, the Reserve Bank of India infused 1 trillion rupees via term repo auction on March 23, 2020.

Thus the RBI ends up with these bonds, that the government themselves issued, and the government now has cash to spend! A non fiat currency cannot do this, as it can in theory, always be exchanged for equal amount of gold. In this system, the new cash is just a promise that the government has made and will eventually pay you (hopefully).

### Step 3: Spending this currency
Now that the government has so much money, it spends it on social work, development, and war. Thus, through this channel, money trickles down to the general population.

### Step 4: The biggest scam by the banks

These people now store their money with the banks. However, banks are not required to store this currency in their vaults. They can lend it forward, invest it in the stock market, or do anything else as long as they can make enogh profit to return your original amount to you with interest and still have some excess left over for themselves.

They still however need to maintain some percentage of it in their vaults. This limit is controlled by the RBI

- Statutory liquidity ratio: The ratio of liquid assets in the form of gold and approved securities that the bank needs to maintain. A higher SLR would mean less liquidity in the market and an ant-inflationary impact. Currently the SLR is 18%
- Cash reserve ratio:  The ratio of cash reserves that banks are required to maintain to ensure their liquidity and solvency. The current rate is 4.5%. Thus for every ₹100 you deposit in the bank, the bank only needs to keep ₹4.5 in the bank, and it can lend out the rest. A decrease in 1% in this rate, will infuse ₹1.37 trillion in the economy.


When you deposit ₹100 in the bank, the bank just keeps ₹4.5 with it, and lends out the rest to someone else. 

Consider the hypothetical situation in which you owned the only ₹100 in existence. You deposit this money in the bank, out of which ₹95.5 is stolen by the bank and given out as a loan to someone else. Now we magically have ₹195.5 in existance. ₹100 in your bank account, and ₹95.5 that the bank just lent out. This excess cash is just in the form of a promise, also known as bank credit, that the bank just made to pay you back. This ₹95.5, is spent to purchase something, and probably comes back to the bank. Which then again, reserves only 4.5% of it, and lends it forward. This ₹100 now becomes

$$\text{₹}100 + \text{₹}100 \cdot (0.955) + \text{₹}100 \cdot (0.955)^2 + \text{₹}100 \cdot (0.955)^3 + \dots = \text{₹}2222.22$$

As this supply of currency in the market increase, the prices of goods shoot up as well. This is what causes **inflation**.

If there were only 1 kg of gold and ₹100 in existence, 1 kg of gold would equal ₹100. However, if the government prints and injects an additional ₹100 into the economy, 1 kg of gold would now cost ₹200; thus, the more currency we have, the more prices rise.

Thus most of the currency in circulation is either pieces of paper, that the government printed or numbers that the bank entered in their system.

### Step 5: Sweating for numbers typed on a computer

We trade away our precious time, for these pieces of papers, and numbers on the computer. It now represents our blood, sweat and time we put in to earn this cash.

> Nothing is certain except death and taxes
{: .prompt-danger }

The income tax department, now decides to tax some(a lot) of this currency you just earned, so that it can be used by the GOI to pay the RBI interest on the bonds, that it bought with the cash that it just printed on a piece of paper!


### Step 6: Paying interest on these numbers

Every process along the way involved lending while increasing the currency supply in circulation. Thus there is some amount of interest due on each rupee that is minted.

Consider the hypothetical situation in which there is no currency and we decide to borrow ₹100 through this system. Although we now have ₹100 out of thin air, we have promised to pay it back with interest. To pay this interest, we must borrow additional funds!

Thus there is never enough currency to pay back all the interest that there is in existance.

> By this means the government may secretly and unobserved, confiscate the wealth of the people, and not one man in a million will detect the theft - [John Maynard Keynes]

The Indian government, currently owes about ₹ 172.50 lakh crore of debt.

![Summary of the Banking System](/assets/images/money/banking_system.svg)
_Summary of the Banking System_
<!-- 
---
title: The banking System
---
flowchart BT
    G -- Pays back interest - -> R
    G[Government] -- Issue bonds - -> A[Swaps bonds] -- Sell to RBI - -> R[RBI]  
    R -- Pays money - -> A -- Pays Money - -> G
    G -- Spends - -> P[People]
    P --  Deposit in bank - -> B2[Lends Cash]
    B2 -- Lend and multiply - -> B2
    B2 -- Lend Money - -> P
    P --  Pay Tax - -> G
    R -- Prints Money - -> R
    subgraph Bank
        direction BT
        A ~~~ B2
    end
 -->


[1]:https://www.businesstoday.in/latest/economy-politics/story/coronovirus-scare-rbi-announces-omos-purchase-of-rs-1-lakh-crore-to-boost-liquidity-252793-2020-03-23