Investor

## Invest

Investor provides funds to cover approved claims with an intent to
earn additional income from insurance premium.

Other investor (sponsor) calls
[submitProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L176)
with parameters:

- `applicant` - address of the proposed investor.  If investor wants to increase his position, `applicant` should be equal to his address
- `sharesRequested` - voting shares requested by this investor,
- `lootRequested` - nonvoting shares requested by this investor, expecte to be zero,
- `tributeOffered` - investment amount,
- `tributeToken` - investment token, should be whitelisted to, say, cDAI,
- `paymentRequested` - should be zero,
- `paymentToken` - should be equal to investment token,
- `details` - url or ipfs hash of investor proposal

After the call, sponsor should call
[sponsorProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L268)
[onlyDelegate](https://github.com/MolochVentures/moloch/tree/master/v1_contracts#onlymemberdelegate)
to sponsor the proposal to start its voting period; the required
amount of the sponsorship deposit is set at the DAO creation.  The
deposit should be made in `depositToken`

After `sponsorProposal` call the proposal is up to voting by existing
investors for `votingPeriodLength` periods followed by
`gracePeriodLength` periods when any disagreing investors can divest
(ragequit).  If the proposal is successful, the sponsorship deposit is
returned to the sponsor minus the processing reward

It is expected that `sharesRequested`/`tributeOffered` rate would
match the rate of currently issued DAO shares (`totalShares`) to DAO
reserves (`GUILD[TOTAL][token]`) or the proposal would be voted down.

## Divest

Investor divests out of the fund by ragequitting.

Investor calls [ragequit](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L528) with parameters:

- `sharesToBurn` - amount of voting shares to burn; should be equal or
  less number of this investor's voting shares
- `lootToBurn` - amount of nonvoting shares to burn; should be equal
or less number of this investor's nonvoting shares

After this call succeedes, investor can withdraw his tokens by calling
[withdrawBalances](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L577)
with parameters:

- `tokens` - list of tokens addresses to be withdrawn
- `amounts` - list of amounts of respective tokens to be withdrawn
- `max`: boolean - set to `true` if withdraw the maximum balance

## Investor votes on claim.

Investor calls [submitVote](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L317) with parameters:

- `proposalIndex` - index of the claim he votes on
- `uintVote` - his vote

## Investor votes on project.

Investor calls [submitVote](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L317) with parameters:

- `proposalIndex` - index of the claim he votes on
- `uintVote` - his vote

## Investor delegates his voting power to another investor.

Not possible in current version of MolochDAO.  No liquid democracy,
every investor should vote himself

## Other callable functions

- [submitWhitelistProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L207)
  could be called by anyone to propose to add another whitelisted
  token
-
  [submitGuildKickProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L219)
  could be called by anyone to propose to kick a member from the DAO;
  if the proposal passes, the member is jailed and can only withdraw
  his fair share of tokens
-
  [processProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L355)
  could be called by anyone to process the specific proposal and get
  `processingReward`
-
  [processWhitelistProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L433)
  could be called by anyone to process the specific token whitelist
  proposal and get `processingReward`
-
  [processGuildKickProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L463)
  could be called by anyone to process the specific kick proposal and
  get `processingReward`
-
  [ragekick](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L563)
  could be called by anyone to actually kick any jailed DAO member
-
  [withdrawBalance](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L573)
  could be called by anyone to withdraw `amount` of `token` balance
  from the DAO
-
  [collectTokens](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L597)
  [onlyDelegate](https://github.com/MolochVentures/moloch/tree/master/v1_contracts#onlymemberdelegate) - allows anyone to collect tribute tokens (see #invest) to the DAO treasury
-
  [cancelProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L609)
  allows caller to cancel the proposal that wasn't sponsored yet
-
  [updateDelegateKey](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L621)
  [onlyShareholder](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L115)
  allows shareholder to update his voting key

