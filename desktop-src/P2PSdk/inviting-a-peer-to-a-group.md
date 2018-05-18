---
Description: 'This topic discusses the process of inviting a peer to join a peer group using the Peer Grouping APIs.'
ms.assetid: '6afcbfec-b1df-45cd-8a43-221dfe5d8c33'
title: Inviting a Peer to a Group
---

# Inviting a Peer to a Group

This topic discusses the process of inviting a peer to join a peer group using the Peer Grouping APIs.

A peer group requires valid credentials to participate. Credentials are issued from outside a group in the form of invitations, or directly to members within a group when credential updates are needed.

## Group Member Certificates

A peer group is created when an application makes a call to [**PeerGroupCreate**](peergroupcreate.md).

To participate in a peer group, each peer must have a peer identity. Call [**PeerEnumIdentities**](peerenumidentities.md) until all peer identities defined for the peer have been returned, and select the one that should be used. If a peer identity does not exist, create one by calling [**PeerIdentityCreate**](peeridentitycreate.md).

Each peer identity is associated with a specific set of credentials that can be used to prove peer group membership when connecting, as well as when publishing records or inviting additional members. These credentials are represented as chains of [X.509 certificates](Http://go.microsoft.com/fwlink/p/?linkid=84413) called Group Membership Certificates (GMC).

To create the GMC for a peer identity, you must first obtain its public key. This key is obtained by calling [**PeerIdentityGetXML**](peeridentitygetxml.md) on the potential invitee and passing in its peer identity. This function returns a base-64 encoded certificate (IDC) that contains the RSA public key used to create the GMC for the peer identity (among other things), encapsulated in an XML blob, in the following format:

``` syntax
<PEERIDENTITYINFO VERSION="1.0">
     <IDC xmlns:dt="urn:schemas-microsoft-com:datatypes" dt:dt="bin.base64">
          <!-- Base-64 encoded certificate  -->
     </IDC>
</PEERIDENTITYINFO>
```

This string can be passed to [**PeerGroupCreateInvitation**](peergroupcreateinvitation.md), which returns an invitation that contains the GMC for that peer identity. The invitation must be passed to the invitee using a different process such as e-mail, FTP, or a secure file share.

Alternatively, the IDC itself can be placed in a new [**PEER\_CREDENTIAL\_INFO**](peer-credential-info.md) structure and passed to [**PeerGroupIssueCredentials**](peergroupissuecredentials.md), which likewise generates an invitation.

Note that applications are not allowed to add tags within the **PEERIDENTITYINFO** tag or modify this XML fragment in any way. Applications are allowed to incorporate this XML fragment into other XML documents, but must strip out all application-specific XML before passing this fragment to the [**PeerGroupCreateInvitation**](peergroupcreateinvitation.md) or [**PeerGroupIssueCredentials**](peergroupissuecredentials.md) functions.

Member GMCs are issued by administrators and the peer group creator. Members must obtain new GMCs with extended lifetimes their GMCs before the expiration time has passed. The peer group administrator issues updated credentials by calling [**PeerGroupIssueCredentials**](peergroupissuecredentials.md) with the existing credentials for that peer.

The [**PEER\_CREDENTIAL\_INFO**](peer-credential-info.md) structure contains the basic data on a peer's membership status, including the public key for their GMC. Newly-issued credentials can be published to the peer group by setting the PEER\_GROUP\_STORE\_CREDENTIALS flag in the call to [**PeerGroupIssueCredentials**](peergroupissuecredentials.md). When the recipient of the new credentials joins the peer group, it's existing credentials will be updated by the Peer Grouping Infrastructure.

## Issuing an Invitation

A member is invited to join the peer group in one of the following two ways:

-   A peer group administrator calls [**PeerGroupCreateInvitation**](peergroupcreateinvitation.md), passing in the identity information XML string obtained from the potential invitee via a common out-of-band mechanism, such as email or an IM session. The invitation is also passed through some external process or mechanism to the peer, who will ultimately receive it as an XML string or text file.
-   A peer group administrator calls [**PeerGroupIssueCredentials**](peergroupissuecredentials.md). To use this function, the peer must have already published membership information to the peer group ([**PEER\_MEMBER**](peer-member.md)), or have an available public key (of the RSA key pair used to create the subject identity). In the former case, the [**PEER\_CREDENTIAL\_INFO**](peer-credential-info.md) structure required for **PeerGroupIssueCredentials** can be obtained from the **PEER\_MEMBER** structure; in the latter case, a new **PEER\_CREDENTIAL\_INFO** structure can be populated with the public key.

After receiving the invitation string, the peer passes it to [**PeerGroupJoin**](peergroupjoin.md) to join the peer group. If the call to **PeerGroupJoin** is successful, the peer can later open the peer group by calling [**PeerGroupOpen**](peergroupopen.md).

## Parsing an Invitation

Optionally, an invitation can be parsed by calling [**PeerGroupParseInvitation**](peergroupparseinvitation.md), which returns a [**PEER\_INVITATION\_INFO**](peer-invitation-info.md) structure. The fields in the structure can be easily obtained for display purposes.

 

 


