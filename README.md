<p align="center">
  <img src="https://www.corda.net/wp-content/uploads/2016/11/fg005_corda_b.png" alt="Corda" width="500">
</p>

# BNO Example

An example of a working BN.

* Deploy the nodes
* Add config for each node under `cordapps/config` in a file called `membership-service.conf`:

    * BNO: `notaryName = "O=Notary,L=London,C=GB"`
    
    * Regular nodes: `bnoWhitelist = ["O=BNO,L=London,C=GB"]`

* Run the nodes
* Run these commands from the node shells:
    * Request membership list as PartyA: `start GetMembersFlow bno: BNO, forceRefresh: false, filterOutNotExisting: false`
        * This will fail as PartyA isn't a member yet
    * Request membership as PartyA: `start RequestMembershipFlow bno: BNO, membershipMetadata: {}`
    * Approve membership as BNO: `start ActivateMembershipForPartyFlow party: PartyA`
    * Request members list as PartyA: `start GetMembersFlow bno: BNO, forceRefresh: false, filterOutNotExisting: false`
        * This will succeed as PartyA is now a member
