<!-- Code generated by gomarkdoc. DO NOT EDIT -->

# gennaro2p

```go
import "github.com/coinbase/kryptology/pkg/dkg/gennaro2p"
```

Wraps dkg/genarro and specializes it for the 2\-party case\. Simpler API\, no distinction between broadcast and peer messages\, and only counterparty messages are used as round inputs since self\-inputs are always ignored\.

## Index

- [type DkgResult](<#type-dkgresult>)
- [type Participant](<#type-participant>)
  - [func NewParticipant(id, counterPartyId uint32, blind *curves.EcPoint, scalar curves.EcScalar, curve elliptic.Curve) (*Participant, error)](<#func-newparticipant>)
  - [func (p *Participant) Finalize(msg *Round2Message) (*DkgResult, error)](<#func-participant-finalize>)
  - [func (p *Participant) Round1(secret []byte) (*Round1Message, error)](<#func-participant-round1>)
  - [func (p *Participant) Round2(msg *Round1Message) (*Round2Message, error)](<#func-participant-round2>)
- [type Round1Message](<#type-round1message>)
- [type Round2Message](<#type-round2message>)


## type [DkgResult](<https://github.com/coinbase/kryptology/blob/master/pkg/dkg/gennaro2p/genarro2p.go#L44-L48>)

```go
type DkgResult struct {
    PublicKey    *curves.EcPoint
    SecretShare  *v1.ShamirShare
    PublicShares map[uint32]*curves.EcPoint
}
```

## type [Participant](<https://github.com/coinbase/kryptology/blob/master/pkg/dkg/gennaro2p/genarro2p.go#L26-L31>)

Participant is a DKG player that contains information needed to perform DKG rounds and yield a secret key share and public key when finished

```go
type Participant struct {
    // contains filtered or unexported fields
}
```

### func [NewParticipant](<https://github.com/coinbase/kryptology/blob/master/pkg/dkg/gennaro2p/genarro2p.go#L54-L55>)

```go
func NewParticipant(id, counterPartyId uint32, blind *curves.EcPoint, scalar curves.EcScalar, curve elliptic.Curve) (*Participant, error)
```

NewParticipant creates a participant ready to perform a DKG blind must be a generator and must be synchronized between counterparties\. The first participant can set it to \`nil\` and a secure blinding factor will be generated\.

### func \(\*Participant\) [Finalize](<https://github.com/coinbase/kryptology/blob/master/pkg/dkg/gennaro2p/genarro2p.go#L126>)

```go
func (p *Participant) Finalize(msg *Round2Message) (*DkgResult, error)
```

Completes the DKG using the counterparty's output from round 2\.

### func \(\*Participant\) [Round1](<https://github.com/coinbase/kryptology/blob/master/pkg/dkg/gennaro2p/genarro2p.go#L83>)

```go
func (p *Participant) Round1(secret []byte) (*Round1Message, error)
```

Runs DKG round 1\. If \`secret\` is nil\, shares of a new\, random signing key are generated\. Otherwise\, the existing secret shares will be refreshed but the privkey and pubkey will remain unchanged\.

### func \(\*Participant\) [Round2](<https://github.com/coinbase/kryptology/blob/master/pkg/dkg/gennaro2p/genarro2p.go#L106>)

```go
func (p *Participant) Round2(msg *Round1Message) (*Round2Message, error)
```

Runs DKG round 2 using the counterparty's output from round 1\.

## type [Round1Message](<https://github.com/coinbase/kryptology/blob/master/pkg/dkg/gennaro2p/genarro2p.go#L33-L38>)

```go
type Round1Message struct {
    Verifiers     []*v1.ShareVerifier
    SecretShare   *v1.ShamirShare
    BlindingShare *v1.ShamirShare
    Blind         *curves.EcPoint
}
```

## type [Round2Message](<https://github.com/coinbase/kryptology/blob/master/pkg/dkg/gennaro2p/genarro2p.go#L40-L42>)

```go
type Round2Message struct {
    Verifiers []*v1.ShareVerifier
}
```



Generated by [gomarkdoc](<https://github.com/princjef/gomarkdoc>)
