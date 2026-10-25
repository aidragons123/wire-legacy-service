# wire-legacy-service

The legacy wire payment service. Flat payment model, no workflow: the checks run inline, one after another (basic validation, duplicate, fraud, bank details, posting), and a fraud-flagged payment is rejected.

* Source: `src/` (plain Java, no build tool needed; `javac` compiles it)
* Main class: `com.bank.wire.legacy.Main`
* Java level: 8
* Protocol: reads one JSON payment per line on stdin and writes one JSON answer per line on stdout, in the same order.
  This is the entry point the comparison agents (Replay Agent, Live Agent) run.

Try it:

```
javac -d out $(find src -name '*.java')
echo '{"requestId":"A1","debtorName":"X","debtorAccount":"123456789","creditorName":"Y","creditorAccount":"987654321","creditorBic":"DEUTDEFF","amount":"100.00","currency":"USD","valueDate":"2030-01-04","processingDate":"2030-01-02"}' | java -cp out com.bank.wire.legacy.Main
```
