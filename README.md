# EinsteinBot_CheckOrderStatus
<h1>To be used in the bot to check order status.</h1>

<b>Some notes on the code:</b>
• The public class OrderInput and OrderOutput are wrapper classes that include all the input and output variables. Each
input and output parameter in these two classes has the @InvocableVariable annotation.

• The getOrderStatus() method has the @InvocableMethod annotation. This method performs a SOQL query to
find the order records by order number, then returns the status. All the extra code using for loops is to make sure that this
method works for bulk invocations.

• The class is public in this sample code. Change the visibility to global if you plan on including this class in a package.


Some of the key considerations for @InvocableVariable and @InvocableMethod are:
• When you open the Bot Builder, all invocable actions in the org are loaded.

• The user-friendly label attribute in an @InvocableMethod annotation is listed in the Bot Builder as the name of the available
action.

• The input and output parameters of the core method have to be List<DataType> because @InvocableMethod needs
a common mechanism to allow the method to be bulk proof. For example, you could have a Process Builder that mass-updates
all children records when a parent record changes. The first element of the output list would be the return value for the first
element of the input list. The second output element maps to the second input element, and so on.
  
• For most use cases, you can get away with not having it be bulk proof. The code can simply operate on the first element of each
input/output list. We made our function bulk proof anyway to illustrate the right way to build the invocable method in case the
code is used in other scenarios.
  
• The public class OrderInput and OrderOutput are optional when you only have one input parameter and one output
parameter. However, if you have more than one input or output parameter, you have to wrap them in a class, as shown in our
example. This is because @InvocableMethod can only take one input parameter. 
  
• If you are using a wrapper class for input and output parameters, make sure to add the @InvocableVariable annotation.
Otherwise the Bot Builder doesn't expose this parameter for you to pass in any data from a variable. For detailed information
and other considerations about @InvocableVariable, see the Apex Developer Guide on the InvocableVariable
Annotation.
  
