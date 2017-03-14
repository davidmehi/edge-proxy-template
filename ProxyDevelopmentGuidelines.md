
## Proxy Development Guidelines

The following are guidelines when developing a proxy.  They can also be used as a checklist to confirm best practice use.  See the Proxy Template example for implementation details.

The proxy will not deploy as is.  Go through the list below to customize before deploying.


1. Name the proxy based on a common proxy naming convention
  1. Example: {businessunit}-{api-purpose/function}-proxy-v1

2. Use a naming convention for policies
  1. Examples:
    1. {policytype}.{purpose}: AssignMessage.SetResponseMessage (recommended)
    2. {policytype}-{purpose}: AM-SetResponseMessage
    3. {flow}.{policytype}.{purpose}: 
      1. GetProfileDetails.AM.SetResponse
      2. GetProfileDetails.AssignMessage.SetResponse
      3. GetProfileDetails-AM-SetResponse

3. Implement common error handling
  1. See FaultRules/DefaultFaultRule
  2. Add additional AssignMessage policies to support additional error codes
  3. FaultRules allow you to customize the error code per error code.
  4. See the policy's documentation for a list of error codes thrown by the policy

4. Use a KVM for environment specific properties.  Proxy should not contain hardcoded urls, credentials or other properties.

5. Use a target server for the backend url
  1. This is needed for 2-way SSL anyways

6. Specify target endpoint path
  1. Specific for each resource
  2. Hardcode if it won't change per environment
  3. Could also use KVM if the target paths may change

7. Use spike arrest to protect against DDOS or other bursts of traffic

8. Leverage custom analytics to capture variables

9. Use catchall flow to catch requests for resources that are not defined.

10. Use consistent variable names throughout the proxy.  Recommended naming convention:
  1. flow.request.{variablename}
  2. flow.kvm.{variablename}

11. Remove unused policies (look for broken chain icon)

12. For major changes to the proxy, be sure to create a new revision before making changes.  


For more best practices, see: <http://docs.apigee.com/api-services/content/best-practices-api-proxy-design-and-development>

*Developing a proxy is only the first part of the software lifecycle.  Don't forget to continue the process with Continuous Integration*


