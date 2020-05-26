Donor:

## Donate funds to risk pool

Donor donates funds to cover approved claims with an intent to support the cause.

Existing investor (sponsor) should call [submitProposal](https://github.com/MolochVentures/moloch/blob/7db370566a5d8c3bad3624700a4ca710c8cf35b4/contracts/Moloch.sol#L176)
with parameters:

- `applicant` - address of the proposed donor
- `sharesRequested` - expected to be zero,
- `lootRequested` - expected to be zero,
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

It is expected that `sharesRequested` and `lootRequested` should be
zero or the proposal would be voted down.
