# Control long-running tasks using timers

## Using timers for delay

The following example illustrates how to use durable timers for delay, which sends a reminder every day for 10 days.

```javascript
const df = require("durable-functions");
const moment = require("moment");

module.exports = df.orchestrator(function*(context) {
    for (let i = 0; i < 10; i++) {
        const deadline = moment.utc(context.df.currentUtcDateTime).add(i, 'd');
        yield context.df.createTimer(deadline.toDate());
        yield context.df.callActivity("SendReminder");
    }
});
```

You should always use currentUtcDateTime to obtain the current date and time, instead of Date.now or Date.UTC.

## Using timers for timeout

The following example illustrates how to use durable timers for a timeout, which will execute a different path if a timeout occurs. In this example, the function waits until either the GetQuote activity function completes or the deadline timer expires. If the activity function completes, the code follows the success case, otherwise, it follows the timeout case.

```javascript
const df = require("durable-functions");
const moment = require("moment");

module.exports = df.orchestrator(function*(context) {
    const deadline = moment.utc(context.df.currentUtcDateTime).add(30, "s");

    const activityTask = context.df.callActivity("GetQuote");
    const timeoutTask = context.df.createTimer(deadline.toDate());

    const winner = yield context.df.Task.any([activityTask, timeoutTask]);
    if (winner === activityTask) {
        // success case
        timeoutTask.cancel();
        return true;
    }
    else
    {
        // timeout case
        return false;
    }
});
```


the next excerise to continue > https://docs.microsoft.com/en-us/learn/modules/create-long-running-serverless-workflow-with-durable-functions/6-exercise-add-a-durable-timer-to-manage-a-long-running-task