

<ac:structured-macro ac:name="info" ac:schema-version="1" ac:macro-id="33bc84c4-e10a-48e7-8e51-05a022b05a36"><ac:parameter ac:name="title">Introduction</ac:parameter><ac:rich-text-body><p>This page is designed to walk through the process of the pros and cons of each. Hopefully, it will help shed some light on each methodology of testing and some scenarios where you would want one over the other.</p></ac:rich-text-body></ac:structured-macro>


Service Virtualization

Service Virtualization is needed when you want to test an <u>application</u> without outside dependencies. This type of test will help you ensure your application is running as expected and reduce the noise on the failures points. What I mean by reduce the noise on the failure points simply means that you would own the data going into your application via Service Virtualization, so you wouldn't need to blame another application for something like poor test data.

<ac:structured-macro ac:name="gliffy" ac:schema-version="1" ac:macro-id="b0c040ef-03fe-48c4-8ae5-d966f5f3a4d7"><ac:parameter ac:name="name">Service Virtualization</ac:parameter><ac:parameter ac:name="pagePin">4</ac:parameter></ac:structured-macro>

### Mocking 

Mocking is needed when you want to test a <u>singular method</u>. The method is isolated from all dependencies to control the scope of the test. This way the test will be maintainable, isolated, and fast. None of that necessarily means the test is good though. Your test is only as good as your asserts but by isolating your method you will have a more consistent pass rate.

<ac:structured-macro ac:name="gliffy" ac:schema-version="1" ac:macro-id="ed23dbb1-ba48-4b26-9f80-2c282b54038a"><ac:parameter ac:name="name">Mocking</ac:parameter><ac:parameter ac:name="pagePin">2</ac:parameter></ac:structured-macro>

### Comparison: 


| <br> | <u>Service Virtualization</u> | <u>Mocking</u> |
| --- | --- | --- |
| <br> | <br> | <br> |
| **Test Speed** | Slower | Faster |
| **Test Maintenance** | Harder | Easier |
| **Test Isolation** | Application Level | <ac:inline-comment-marker ac:ref="51e75a01-51f7-4138-9ec1-5f7b0b2e42ce">Method Level</ac:inline-comment-marker> |
| **Application Configuration** | Full | Partial |
| **Test Data Artifacts** | Yes | No |
| **Testing Dependency Contracts** | Easier | Harder |
| **Live Implementation** | Yes | No |
| **Code Coverage** | No | Yes |




### Conclusion

Though each has its pros and cons I hope you can see the similarities between the two methods of testing. For Example, some scenarios call for a full configuration of you application for testing and some scenarios can easily be tested with a isolated configuration. Neither form of testing is the golden bullet of test methodology, they are both different tools for different situations. Always choose the right methodology when it fits your needs but remember to "Do The Right Thing", the right methodology may not always be the easiest to adopt.


