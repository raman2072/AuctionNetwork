# AuctionNetwork
Yet another Hyperledger Fabric/Composer POC - this time illustrating Assets Tranfer

This POC introduces more complexity in using Composer to define the smart contract. 
This POC deals with how to add multiple participants and add access control to a  blockchain application. 
To do that - we will create an interactive, distributed, product auction demo network. 
We will list assets for sale (setting a reserve price) and watch as assets that have met their reserve price are automatically 
transferred to the highest bidder at the end of the auction. Also each participant will have different level of access 
permissions depending on the Access Control Rules (ACL) in permissions.acl file. 
Access Control Lists (ACL) are the settings for sharing and privacy, which are automatically enforced by the Fabric Composer 
runtime. This POC has been successfully tested and runs on Hyperledger Composer V0.19.6, Hyperledger Fabric V1.1.

This business network defines:

Participants: Member Seller

Assets: Product ProductListing

Transactions: AddProduct StartBidding Offer CloseBidding

The addProduct function is called when an AddProduct transaction is submitted. The logic allows a seller to create a product 
asset and update its registry.

The publishListing function is called when a StartBidding transaction is submitted by the owner of product. The logic allows a 
seller to create a smart contract in the form of product listing for their product with a reserve bid.

The makeOffer function is called when an Offer transaction is submitted. The logic simply checks that the listing for the offer
is still for sale, and then adds the offer to the listing, and then updates the offers in the ProductListing asset registry.

The closeBidding function is called when a CloseBidding transaction is submitted for processing. The logic checks that the 
listing is still for sale, sort the offers by bid price, and then if the reserve has been met, transfers the ownership of the 
product associated with the listing to the highest bidder. Money is transferred from the buyer's account to the seller's account, and then all the modified assets are updated in their respective registries.

product.cto file present in models directory defines a data model for the product auction demo which consists the definition 
for assets, participants and transactions. logic.js file present in lib directory implement the transactions defined in the 
product.cto file. Recall that the .cto file defines the structure of your business network in terms of Assets, Participants 
and Transactions.

ACL rules are present in permissions.acl file to determine which user/role is permitted to create, read, update or delete an 
element in the business network's domain model. The default System user has all the permissions. Members of the network have 
read access to all the resources and the seller can create a product, start and close the bidding for their products. Members
of the network can make their bid for the product listing. Participants can access only permitted resources and transactions.
