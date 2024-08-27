Cisco FMC will not delete a network object if it in still associated with an \ 
access policy / access rule.

The deleteNetworkObject.yml playbook contains logic to determine the Access Polices where the Network Object \
exists.  This can be used where you may have a significant number of Acecss Policies to limit the Policies that need to be searched for the Network Object.


There are three main yaml file associated with this demonstration of using the Cisco FMC collection:
- getAllAccessPolicies.yml playbook gets the domain data, and all access policies, runs tasks in getAccessRules.yml.  After running through the included tasks and deleting the network object from access rules, it will delete the network object.
- getAccessRules.yml playbook gets all the access rules from an access policy, runs tasks in getAccessRule.yml
- getAccessRule.yml gets information about the rule, uncluding whether the network object is in the rule, and proceeds to delete the network object.

These playbooks provide an example of how to use the Cisco FMC modules to:
- Search through access policies / access rules for a network object
- Remove the network object from the access rule without deleting the access rule \
  or any other network objects in the access rule
- Delete the network object


Test:
- Deploy an FMC sandbox in the devnetsandbox.cisco.com.  This requires a Cisco or github login.
- Update the inventory file to include the username and password provided by the sandbox.
- I did a filter in the getAllAccessPolicies.yml playbook to make my testing faster, but it is commented out.  Testing was conducted successfully with this commented out.
- Run the access_rule_create.yml playbook to create network objects, and add network objects to an access rule in an access policy - if this Access Policy does not exist, then it will fail; use one that does exist.
- Run the getAllAccessPolicies.yml playbook to find and remove the network objects, and then delete the network object.




