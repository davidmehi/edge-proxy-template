# edge-proxy-template
Details an Apigee Edge proxy template incorporating best practices

This template has best practices built into the proxy.  A developer can use this template as their starting point in creating a proxy.  Save as a new proxy and customize.

Steps to customize:

1. Enforce API Key or AccessToken Verification
  1. Enable a secure API by either API or Access token
  2. Be sure to add one of these in the preflow
2. Enforce Spike Arrest policy and the Quota policy
3. Extract the necessary request headers, parameters, path parameters and/or payload data
  a. Reference the "ExtractVariables.CommonRequestHeaders" policy
4. Fill in the necessary resource flows.
  a. Replace "getResource" and "postResource" with your resource and verb definitions
5. Add necessary validation
  a. Use the "Javascript.ValidateRequestParameters" policy as a guide.  This provides a robust way to validate request headers, parameters, path parameters and payloads using Javascript
  b. Add the validation to each resource that needs it.  You will need to create a copy of this policy for each instance
  c. Use JSON threat protection on POST calls
6. Set Target Server
  a. Define your Target Server using the Management UI or Management API.
  b. Reference the target server in the "Default Target Endpoint"
    i. <Server name="TargetServerName"/>
7. Set Target Path
  a. Each resource path should define the target path.
  b. If the target path changes per environment, then use the KVM to store the target path
  c. If it does not change per environment, then use an AssignMessage or Javascript policy to set the target path
  d. Refer to "AssignMessage.SetGetResourceTargetPath" for how to set a value for the "flow.request.targetPath" variable
8. Use KVM if needed
  a. Create KVM for environment in the Management UI or API
  b. Refer to the "KeyValueMap.GetConfigSettings" policy for KVM reference
  c. Modify the mapIdentifier="APIConfig" setting in the policy.  This should be the name of the KVM you created.
9. Set VirtualHost in proxy default to match the correct VirtualHost.
  a. This should be an https host.  The default https host is "secure".  If you created a custom VirtualHost, use that name instead.  
10. Enhance Error Handling if needed
  a. If you have added new policies or need to handle extra types of Faults, refer to the FaultRules and DefaultFaultRule flow in the default proxy endpoint
  b. Edit the "FaultRules.DefaultErrorResponse" to change the format of the error response
11. Leverage Custom Analytics if required
  a. Reference the "Stats.RecordCustomAnalytics"


