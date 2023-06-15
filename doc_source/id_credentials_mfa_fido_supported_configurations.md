# Supported configurations for using FIDO security keys<a name="id_credentials_mfa_fido_supported_configurations"></a>

You can use WebAuthn as a multi\-factor authentication \(MFA\) method with IAM using currently supported configurations\. These include FIDO Certified devices supported by IAM and browsers that support WebAuthn\.

## FIDO devices supported by AWS<a name="id_credentials_mfa_fido_supported_devices"></a>

IAM currently supports FIDO Certified security devices that connect to your devices through USB, Bluetooth, or NFC\. We currently do not support platform authenticators such as TouchID, FaceID, or Windows Hello\.

**Note**  
AWS requires access to the physical USB port on your computer to verify your FIDO Certified device\. WebAuthn MFA will not work with a virtual machine, a remote connection, or a browser's incognito mode\.

The FIDO Alliance maintains a list of all [FIDO Certified products](https://fidoalliance.org/certification/fido-certified-products/) that are compatible with FIDO specifications\.

## Browsers that support WebAuthn<a name="id_credentials_mfa_fido_browsers"></a>

The following browsers currently support the use of FIDO Certified security keys:


****  

|  | macOS 10\.15\+ | Windows 10 | Linux | 
| --- | --- | --- | --- | 
| Chrome | Yes | Yes | Yes | 
| Safari | Yes | No | No | 
| Edge | Yes | Yes | Yes | 
| Firefox | Yes | Yes | Yes | 

**Note**  
Most Firefox versions that currently support WebAuthn don't enable support by default\. For instructions on enabling WebAuthn support in Firefox, see [Troubleshooting FIDO security keys](troubleshoot_mfa-fido.md)\.

### Browser plugins<a name="id_credentials_mfa_fido_plugins"></a>

AWS currently supports only browsers that natively support the FIDO2/WebAuthn standard\. AWS does not support using plugins to add FIDO2/WebAuthn browser support\. Also note that some browser plugins are incompatible with the U2F standard and can cause unexpected results with FIDO2 security keys\. 

For information on disabling browser plugins and other troubleshooting tips, see [I can't enable my FIDO security key](troubleshoot_mfa-fido.md#troubleshoot_mfa-fido-cant-enable)\. 

## Mobile environments<a name="id_credentials_mfa_fido_mobile_environments"></a>

The following browsers currently support the use of FIDO Certified security keys: 


****  

|  | iOS 14\.5\+ | Android 7\+ | 
| --- | --- | --- | 
| Chrome | Yes | Yes | 
| Safari | Yes | No | 
| Edge | No | No | 
| Firefox | Yes | No | 

**Note**  
The AWS Console Mobile App does not currently support using FIDO certified security keys for MFA\.

## AWS CLI and AWS API<a name="id_credentials_mfa_fido_cliapi"></a>

AWS currently supports using FIDO certified security keys only in the AWS Management Console\. Using FIDO Certified security keys for MFA is not currently supported in the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/) and [AWS API](https://aws.amazon.com/tools/), or for access to [MFA\-protected API operations](id_credentials_mfa_configure-api-require.md)\.

## Additional resources<a name="id_credentials_mfa_fido_additional_resources"></a>
+ For more information on using FIDO certified security keys in AWS, see [Enabling a FIDO security key \(console\)](id_credentials_mfa_enable_fido.md)\.
+ For help with troubleshooting FIDO in AWS, see [Troubleshooting FIDO security keys](troubleshoot_mfa-fido.md)\.
+ For general industry information on FIDO support, see [FIDO2 Project](https://en.wikipedia.org/wiki/FIDO2_Project)\. 