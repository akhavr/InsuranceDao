# Insurance DAO

Goal: allow entities unite to protect against the risk of individual events (as opposed to market events)

Design principles: start from simplest possible thing to prove technical feasibility, product-market fit, and minimize security surface.

## Roles

- investor
- donor
- insurance holder
- summoner

Summoner is an entity that creates the insurance DAO and votes to
appoint initial investor.  The rest of roles is obvious.

An entity can be any combination of these roles.

V2: Actuary and Underwriter.  To support different insurance prices, depending on a holder's risk profile, actuary should be able to asses holder's risk and underwrite the higher/lower premium on this particular insurance.

## Insurance

Each insurance has:

- type
- duration
- premium paid
- amount insured
- state

## Fund usage

- hold passive interest (e.g. in Compound)
- pay out insured amount on approved claiims
- finance projects
- pay out dividends

## DAO

Each DAO
- sells a single type of insurance with a fixed duration
- has cap on the AUM (assets under management)

V1 supports only fixed insurance price with fixed amount insured and binary outcome (approved/rejected).

That implies that holders are expected to have pretty uniform risk profile.  Thus, investors approve each holder insurance individually.

V1: Fund participation is not transferable.  Only way to divest is to ragequit.  V2 supports tokenized transferable participation.

V2 should support different insurance prices depending on a holder's risk profile via actuary/underwriter staking.

V2 - automated claim processing?

## Usecases

Investor:

1. Investor provides funds to cover approved claims with an intent to earn additional income from insurance premium.
2. Investor divests out of the fund by ragequitting.
3. Investor votes on claim.
4. Investor votes on project.
5. Investor delegates his voting power to another investor.

Donor:

1. Donor provides funds to cover approved claims and to fund projects as a donation.  There's nothing else a donor can do.

Holder:

1. Holder buys an insurance.
2. Holder submits a claim.

## Open questions

1. What happens with the DAO and insurance holders if all investors ragequit?
2. How to set the insurance cost?
3. Should the DAO be time-limited?
4. Should there be a quorum on votes?

## FAQ

Q. What about fradulent claims?
A. In Ukraine around 30% claims are considered being fradulent.  This is still an open area of research, therefore in V1 of DAO each insurance is sold only after investors approval.

Q. Why people would buy insurance from a non-reputable provider?
A. Reputation is subjective.  Your insurance DAO would be able to build its reputation by clear claim policies, history of payments, and, optionally, selling cover of risks that "legal" and "reputable" companies can't sell.

Q. How investors would be protected from legal risks?
A.
- Option 1: register DAO as LAO and get legal protection
- Option 2: buy insurance in another DAO against legal risks
- Option 3a: create DAO based on zkDAI (aztec protocol)
- Option 3b: invest through tornado.cash (into existing DAO)

Q. In the suggested model investors hold all risks.  Meanwhile, in current western insurance model, 70%-80% of paid claims are reimbursed via reinsurance and/or regress claim.  How this would be solved?
A. A finace model of current western insurance company is based on developed risk markets.  Now risk markets in crypto are in a nascent stage.  When they would have sufficient liquidity, DAO investors would be able to buy such products using "finance the project" option.
