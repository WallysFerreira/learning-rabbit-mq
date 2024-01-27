# Topic exchange

Topic exchanges are similar to direct exchanges except their binding key is actually a list of words, so it can route messages based on multiple conditions instead of only one.

The list of words should be separated with dots (".") and the limit of the list is 255 bytes.

Topic exchanges' binding keys also accept two special characters:
- "*" (star) substitues exactly one word
- "#" (hash) substitutes zero or more words


## Examples

- If a queue is bounded to a direct exchange with binding key "#", it will match all messages, behaving like a fanout exchange.
- When binding a queue to a direct exchange without using the special characters on the binding key, like "pastel", it will behave like a direct exchange.
- Binding a queue to a direct exchange with binding key "*.pastel", it will match messages with routing keys like "something.pastel" 
- Binding a queue to a direct exchange with binding key "pastel.#", it will match messages with routing keys like "pastel.testing" or "pastel.testing.something" 
