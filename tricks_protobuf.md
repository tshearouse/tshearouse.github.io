## Protobuf tips
Things I discover and then forget, repeatedly.
 - Proto does bit packing. Stop looking for 'short', 'uint8', or other variants to save you a few bits. There's nothing smaller than int32.
 - uint32/64 exists, and still does bit packing.
 - sint32/64 is functionally equivalent to int32/64, but sint is more efficient at storing negative numbers.
 - Yes, there is a map type. The key must be a integral or string type. 
	 - Code will generate silly. You'll get an inner type that has 'key' and 'value' properties, instead of a Map or Dictionary.
	 - Do not decide to avoid maps just because the code generates strangely. Yes, you get better names if you replace a map with a list of some custom message (that has its own well-named properties for 'key' and 'value'). But the map packs much better. Presumably this is because you're not storing message headers?
 - Enums must contain a '0' value as the first entry. Most codegen tools won't complain if you violate this. You'll discover it the first time you try to serialize data that has an un-set optional enum.
