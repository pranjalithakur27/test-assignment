# test-assignment
1. Start up the Fabric test network with Certificate Authorities and CouchDB:
```
./network.sh up createChannel -ca -s couchdb 
```
2. Deploy the private data smart contract to the channel:
```
./network.sh deployCC -ccn private -ccp ./asset-transfer-private-data/chaincode-go/ -ccl go -ccep "OR('Org1MSP.peer','Org2MSP.peer')" -cccg ./asset-transfer-private-data/chaincode-go/collections_config.json
```
3. Register identities:
```
export PATH=${PWD}/../bin:${PWD}:$PATH
export FABRIC_CFG_PATH=$PWD/../config/
```
```
export FABRIC_CA_CLIENT_HOME=${PWD}/organizations/peerOrganizations/org1.example.com/
```
```
fabric-ca-client register --caname ca-org1 --id.name owner --id.secret ownerpw --id.type client --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem
```
```
fabric-ca-client enroll -u https://owner:ownerpw@localhost:7054 --caname ca-org1 -M
${PWD}/organizations/peerOrganizations/org1.example.com/users/owner@org1.example.com/msp --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem
```
```
cp ${PWD}/organizations/peerOrganizations/org1.example.com/msp/config.yaml ${PWD}/organizations/peerOrganizations/org1.example.com/users/owner@org1.example.com/msp/config.yaml
```
```
export FABRIC_CA_CLIENT_HOME=${PWD}/organizations/peerOrganizations/org2.example.com/
```
```
fabric-ca-client register --caname ca-org2 --id.name buyer --id.secret buyerpw --id.type client --tls.certfiles ${PWD}/organizations/fabric-ca/org2/tls-cert.pem
```
```
fabric-ca-client enroll -u https://buyer:buyerpw@localhost:8054 --caname ca-org2 -M ${PWD}/organizations/peerOrganizations/org2.example.com/users/buyer@org2.example.com/msp --tls.certfiles ${PWD}/organizations/fabric-ca/org2/tls-cert.pem
```
```
cp ${PWD}/organizations/peerOrganizations/org2.example.com/msp/config.yaml ${PWD}/organizations/peerOrganizations/org2.example.com/users/buyer@org2.example.com/msp/config.yaml
```

