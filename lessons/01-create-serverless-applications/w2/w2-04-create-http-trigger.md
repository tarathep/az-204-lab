# Create an HTTP trigger

1. at azure portal go to azure function and then create function app.

2. select a template section, select HTTP trigger.

3. template details section, in ``New Function`` enter Authorization level select ``Anonymous``

![](../../media/l-4.png)

4. select Code + Test, and review the auto-generated code to get an idea about what's going on. The req parameter represents the incoming request and contains a name parameter. Check to see if name has a value. If it does, we return a greeting. Otherwise, it continues to ask for a value.

![](../../media/l-5.png)

![](../../media/l-6.png)

![](../../media/l-7.png)
