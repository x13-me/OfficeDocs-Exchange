---
localization_priority: Normal
description: 'How to leverage S/MIME to sign and encrypt messages when using Outlook for iOS and Android.'
ms.topic: article
author: msdmaguire
ms.author: dmaguire
title: Outlook for iOS sensitive labeling, Outlook for Android sensitive labeling, Outlook for iOS S/MIME, Outlook for Android S/MIME
ms.reviewer: smithre4
audience: ITPro
ms.service: exchange-online
manager: serdars

---

# S/MIME in Outlook for iOS and Android

**Summary**: How to leverage S/MIME to sign and encrypt your messages when using Outlook for iOS and Android.

Protecting company or organizational data is extremely important. One solution for protecting message content is Secure/Multipurpose Internet Mail Extension (S/MIME). Mobile messaging applications like Outlook for iOS and Android work in conjunction with S/MIME to sign and encrypt Office 365 message data.

S/MIME provides encryption, which protects the content of e-mail messages, and it provides digital signatures, which verify the identity of the sender of an e-mail message. S/MIME in Outlook for iOS and Android is supported with Office 365 accounts using the native Microsoft sync technology.

## Understanding S/MIME

Digital signatures are the more commonly used service of S/MIME. As the name suggests, digital signatures are the digital counterpart to the traditional, legal signature on a paper document. As with a legal signature, digital signatures provide the following security capabilities:

  - **Authentication:** A signature serves to validate an identity. It verifies the answer to "who are you" by providing a means of differentiating that entity from all others and proving its uniqueness. Because there is no authentication in SMTP e-mail, there is no way to know who sent a message. Authentication in a digital signature solves this problem by allowing a recipient to know that a message was sent by the person or organization who claims to have sent the message.

  - **Nonrepudiation:** The uniqueness of a signature prevents the owner of the signature from disowning the signature. This capability is called nonrepudiation. Thus, the authentication that a signature provides gives the means to enforce nonrepudiation. The concept of nonrepudiation is most familiar in the context of paper contracts: a signed contract is a legally binding document, and it is impossible to disown an authenticated signature. Digital signatures provide the same function and, increasingly in some areas, are recognized as legally binding, similar to a signature on paper. Because SMTP e-mail does not provide a means of authentication, it cannot provide nonrepudiation. It is easy for a sender to disavow ownership of an SMTP e-mail message.

  - **Data integrity:** An additional security service that digital signatures provide is data integrity. Data integrity is a result of the specific operations that make digital signatures possible. With data integrity services, when the recipient of a digitally signed e-mail message validates the digital signature, the recipient is assured that the e-mail message that is received is, in fact, the same message that was signed and sent, and has not been altered while in transit. Any alteration of the message while in transit after it has been signed invalidates the signature. In this way, digital signatures provide an assurance that signatures on paper cannot, because it is possible for a paper document to be altered after it has been signed.

> [!IMPORTANT]
> Although digital signatures provide data integrity, they don't provide confidentiality. Messages with only a digital signature are sent in cleartext, like SMTP messages and can be read by others. In the case where the message is opaque-signed, a level of obfuscation is achieved because the message is base64-encoded, but it is still cleartext. To protect the contents of e-mail messages, encryption must be used.

Message encryption provides a solution to information disclosure. SMTP-based Internet e-mail does not secure messages. An SMTP Internet e-mail message can be read by anyone who sees it as it travels or views it where it is stored. These problems are addressed by S/MIME using encryption. Encryption is a way to change information so that it cannot be read or understood until it is changed back into a readable and understandable form. Message encryption provides two specific security services:

  - **Confidentiality**: Message encryption serves to protect the contents of an e-mail message. Only the intended recipient can view the contents, and the contents remain confidential and cannot be known by anyone else who might receive or view the message. Encryption provides confidentiality while the message is in transit and in storage.

  - **Data** **integrity:** As with digital signatures, message encryption provides data integrity services as a result of the specific operations that make encryption possible.

> [!IMPORTANT]
> Although message encryption provides confidentiality, it doesn't authenticate the message sender in any way. An unsigned, encrypted message is as susceptible to sender impersonation as a message that isn't encrypted. Because nonrepudiation is a direct result of authentication, message encryption also doesn't provide nonrepudiation. Although encryption does provide data integrity, an encrypted message can show only that the message hasn't been altered since it was sent. No information about who sent the message is provided. To prove the identity of the sender, the message must use a digital signature.

## Deploying S/MIME certificates with Outlook for iOS and Android

> [!NOTE]
> At this time, S/MIME is supported only in Outlook for iOS. Outlook for Android will receive S/MIME support in a future release. For more information, see the [Microsoft 365 Roadmap](http://aka.ms/m365roadmap).

First, ensure S/MIME has been properly configured in Exchange Online by following the steps outlined in [S/MIME for message signing and encryption in Exchange Online](https://docs.microsoft.com/office365/SecurityCompliance/s-mime-for-message-signing-and-encryption). This includes setting up the virtual certificate collection and publishing the certificate revocation list to the Internet.

Once those steps have been completed, S/MIME certificates can be deployed to Outlook for iOS and Android via the following ways:

1. Automated certificate delivery (future release).

2. Manual certificate delivery.

> [!NOTE]
> Outlook for iOS and Android will support automated certificate delivery in future releases. For more information, see the [Microsoft 365 Roadmap](http://aka.ms/m365roadmap).

In both delivery solutions, it is expected that the certificate’s trusted root chain is available and discoverable within Exchange Online. Trust verification is performed on all digital certificates. Exchange Online validates the certificate by validating each certificate in the certificate chain until it reaches a trusted root certificate. In most cases, this is done by obtaining the intermediate certificates through the authority information access path in the certificate until a trusted root certificate is located. Intermediate certificates can also be included with digitally signed e-mail messages. If Exchange Online locates a trusted root certificate and can query the certificate revocation list for the certificate authority, the digital certificate's chain for that digital certificate is considered valid and trusted and can be used. If Exchange Online fails to locate a trusted root certificate or fails to contact the certificate revocation list for the certificate authority, that certificate is considered invalid and not trusted.

Outlook for iOS and Android leverages the user’s primary SMTP address for mail flow activities which is configured during account profile setup. The S/MIME certificate used by Outlook for iOS and Android is calculated by comparing the user’s primary SMTP address as defined in the account profile with the certificate’s subject value or the subject alternative name value; if these do not match, then Outlook for iOS and Android will report that a certificate is not available (see Figure 7) and not allow the user to sign and/or encrypt messages.

> [!IMPORTANT]
> Outlook for iOS and Android S/MIME functionality requires that a user have both signing and encrypting capabilities which can be delivered with a single certificate or with separate signing and encryption certificates.

### Manual Certificate Delivery

Outlook for iOS and Outlook for Android both support manual certificate delivery, which is when the certificate is emailed to the user and the user taps on the certificate attachment within the app to initiate the certificate’s installation. The following image shows how manual certificate delivery works in iOS.

![Screen shots showing manual certificate installation on iOS.](../../media/sensitive-manual-certificate.png)

A user can export their own certificate and mail it to themselves using Outlook. For more information, see [Exporting a digital certificate](https://support.office.com/article/f3574266-2f9e-4f15-ab21-5989f4cf0c9b).

> [!IMPORTANT]
> When exporting the certificate, ensure that the exported certificate is password-protected with a strong password.

### Enabling S/MIME in the client

S/MIME must be enabled for Outlook for iOS and Android to view or create S/MIME-related content.

End users will need to enable S/MIME functionality manually by accessing their account settings, tapping Security, and tapping the S/MIME control, which is off by default. The Outlook for iOS S/MIME security setting looks like the following:

![Screen shots showing Outlook for iOS S/MIME security settings.](../../media/sensitive-s-mime-setting.png)

When the S/MIME setting is enabled, Outlook for iOS and Android will automatically disable the **Organize By Thread** setting. This is because S/MIME encryption becomes more complex as a conversation thread grows. By removing the threaded conversation view, Outlook for iOS and Android reduces the opportunity for issues with certificates across recipients during signing and encryption. As this is an app-level setting, this change affects all accounts added to the app. This threaded conversation dialog is rendered in iOS as follows:

![Screen shot showing the OUtlook for iOS threaded conversation dialog.](../../media/sensitive-ios-threaded-con.png)

## Using S/MIME in Outlook for iOS and Android

After the certificates have been deployed and S/MIME has been enabled in the app, users can consume S/MIME related content and compose content using S/MIME certificates. If the S/MIME setting is not enabled, then users will not be able to consume S/MIME content.

### Consumption

In the message view, users can view messages that are S/MIME signed or encrypted. In addition, users can tap the S/MIME status bar to view more information about the message’s S/MIME status. The following screen shots show examples of how S/MIME messages are consumed in Android.

> [!IMPORTANT]
> In order to read an encrypted message, the recipient’s private certificate key must be available on the device.

![Screen shots of S/MIME usage in iOS.](../../media/sensitive-ios-s-mime.png)

Users can install a sender’s public certificate key by tapping the S/MIME status bar. The certificate will be installed on the user’s device, specifically in the Microsoft publisher [keychain in iOS](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) or the system [KeyStore in Android](https://source.android.com/security/reports/Google_Android_Enterprise_Security_Whitepaper_2018.pdf). The Android version appears similar to the following:

![Screen shots of Outlook for Android public key installation](../../media/sensitive-android-key-install.png)

If there are certificate errors, Outlook for iOS and Android will warn the user. The user can tap the S/MIME status bar notification to view more information about the certificate error, such as in the following example.

![Screen shot of Outlook for iOS cert error on received message.](../../media/sensitive-cert-error-message.png)

### Composition

Before a user can send a signed and/or encrypted message, Outlook for iOS and Android performs a validity check on the certificate to ensure it's valid for signing or encryption operations. If the certificate is near expiration, Outlook for iOS and Android will alert the user to obtain a new certificate when the user attempts to sign or encrypt a message, beginning 30 days before expiration.

![Screen shots showing warnings about certificate expiration.](../../media/sensitive-android-cert-warning.png)

When composing an email in Outlook for iOS and Android, the sender can choose to encrypt and/or sign the message. By tapping on the **ellipses** and then **Sign and Encrypt**, the various S/MIME options are presented. Selecting an S/MIME option enables the respective action on the email when it is sent (drafts are not signed or encrypted), assuming the sender has a valid certificate.

> [!NOTE]
> Outlook for iOS and Android only supports sending clear-signed messages.

> [!IMPORTANT]
> In order to compose an encrypted message, the target recipient’s public certificate key must be available either in the Global Address List or stored on the local device. In order to compose a signed message, the sender’s private certificate key must be available on the device.

Here is how S/MIME options appear in Outlook for Android:

![Screen shots of Outlook for Android S/MIME options.](../../media/sensitive-android-smime-options.png)

Outlook for iOS and Android will evaluate all recipients prior to sending an encrypted message and confirm that a valid public certificate key exists for each recipient. The Global Address List (GAL) is checked first; if a certificate for the recipient does not exist in the GAL, Outlook queries the Microsoft publisher keychain in iOS or the system KeyStore in Android to locate the recipient’s public certificate key. For recipients without a public certificate key (or an invalid key), Outlook will prompt for their removal. The message will not be sent without encryption to any recipient unless the encryption option is disabled by the sender during composition.

![Screen shot of Outlook for iOS warning about recipient certificates.](../../media/sensitive-ios-no-cert-warning.png)
