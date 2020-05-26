Holder:

## Holder buys an insurance

Holder pays a premiuum for the insurance.

Holder calls [submitProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L176)
with parameters:

- `applicant` - address of the proposed holder
- `sharesRequested` - voting shares requested by this holder, should be zero,
- `lootRequested` - nonvoting shares requested by this investor, should be zero,
- `tributeOffered` - premium amount,
- `tributeToken` - premium token, should be whitelisted to, say, cDAI,
- `paymentRequested` - should be zero,
- `paymentToken` - should be equal to investment token,
- `details` - url or ipfs hash of holder details

After the call, existing investor (sponsor) should call
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

It is expected that `tributeOffered` would be enough to keep DAO funds
(`GUILD[TOTAL][token]`) at 100% reserve or above, or the proposal
would be voted down.

DAO reserve rate is is calculated as amount of all potential claims
divided by DAO reserves (`claim amount` * `number of insurance
holders` / `GUILD[TOTAL][token]`)

## Holder submits a claim

Holder calls [submitProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L176)
with parameters:

- `applicant` - his address
- `sharesRequested` - voting shares requested by this holder, should be zero,
- `lootRequested` - nonvoting shares requested by this investor, should be zero,
- `tributeOffered` - tribute offered, should be zeero,
- `tributeToken` - premium token, should be whitelisted to, say, cDAI,
- `paymentRequested` - should be equal to the claim amount,
- `paymentToken` - should be equal to `tributeToken`,
- `details` - url or ipfs hash of the claim details

After the call, existing investor (sponsor) should call
[sponsorProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L268)
[onlyDelegate](https://github.com/MolochVentures/moloch/tree/master/v1_contracts#onlymemberdelegate)
to sponsor the claim to start its voting period; the required amount
of the sponsorship deposit is set at the DAO creation.  The deposit
should be made in `depositToken`

After `sponsorProposal` call the claim is up to voting by existing
investors for `votingPeriodLength` periods followed by
`gracePeriodLength` periods when any disagreing investors can divest
(ragequit).  If the claim is successful, the sponsorship deposit is
returned to the sponsor minus the processing reward.

If the claim is successful, the holder can withdraw his tokens by calling
[withdrawBalances](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L577)
with parameters:

- `tokens` - list of tokens addresses to be withdrawn
- `amounts` - list of amounts of respective tokens to be withdrawn
- `max`: boolean - set to `true` if withdraw the maximum balance
