[TOC]

This document lists all detectors in SpotBugs.

Standard detectors
-----------------------------------------------------------------

These detectors are on by default:

### OverridingMethodsMustInvokeSuperDetector

Finds overriding methods that must call super.

*   [CN: Super method is annotated with @OverridingMethodsMustInvokeSuper, but the overriding method isn’t calling the super method. (OVERRIDING\_METHODS\_MUST\_INVOKE\_SUPER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#overriding-methods-must-invoke-super)


### FindRoughConstants

Finds constants which roughly (but not precisely) equal to known values like Math.PI.

*   [CNT: Rough value of known constant found (CNT\_ROUGH\_CONSTANT\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#cnt-rough-constant-value)


### SynchronizeAndNullCheckField

This detector looks for a field that is synchronized on and then null checked.

*   [NP: Synchronize and null check on the same field. (NP\_SYNC\_AND\_NULL\_CHECK\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-sync-and-null-check-field)


### InitializeNonnullFieldsInConstructor

Finds non-null fields that are not written to in constructors.

*   [NP: Non-null field is not initialized (NP\_NONNULL\_FIELD\_NOT\_INITIALIZED\_IN\_CONSTRUCTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-nonnull-field-not-initialized-in-constructor)


### BooleanReturnNull

Looks for methods with Boolean return type that return explicit null values.

*   [NP: Method with Boolean return type returns explicit null (NP\_BOOLEAN\_RETURN\_NULL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-boolean-return-null)


### OptionalReturnNull

Looks for methods with Optional return type that return explicit null values.

*   [NP: Method with Optional return type returns explicit null (NP\_OPTIONAL\_RETURN\_NULL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-optional-return-null)


### ConfusionBetweenInheritedAndOuterMethod

Looks for potential confusion between inherited and outer methods.

*   [IA: Potentially ambiguous invocation of either an inherited or outer method (IA\_AMBIGUOUS\_INVOCATION\_OF\_INHERITED\_OR\_OUTER\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ia-ambiguous-invocation-of-inherited-or-outer-method)


### SynchronizationOnSharedBuiltinConstant

This detector looks for synchronization on a shared built-in constant (such as a String).

*   [DL: Synchronization on Boolean (DL\_SYNCHRONIZATION\_ON\_BOOLEAN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dl-synchronization-on-boolean)

*   [DL: Synchronization on boxed primitive (DL\_SYNCHRONIZATION\_ON\_BOXED\_PRIMITIVE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dl-synchronization-on-boxed-primitive)

*   [DL: Synchronization on interned String (DL\_SYNCHRONIZATION\_ON\_INTERNED\_STRING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dl-synchronization-on-interned-string)

*   [DL: Synchronization on String literal (DL\_SYNCHRONIZATION\_ON\_SHARED\_CONSTANT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dl-synchronization-on-shared-constant)

*   [DL: Synchronization on boxed primitive values (DL\_SYNCHRONIZATION\_ON\_UNSHARED\_BOXED\_PRIMITIVE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dl-synchronization-on-unshared-boxed-primitive)


### NoteUnconditionalParamDerefs

Analyze all methods in the application to determine which dereference parameters unconditionally. This information is used in a later analysis pass to find call sites where null values may be passed to those methods.

This is a slow detector.

*   [NP: equals() method does not check for null argument (NP\_EQUALS\_SHOULD\_HANDLE\_NULL\_ARGUMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-equals-should-handle-null-argument)

*   [NP: Parameter must be non-null but is marked as nullable (NP\_PARAMETER\_MUST\_BE\_NONNULL\_BUT\_MARKED\_AS\_NULLABLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-parameter-must-be-nonnull-but-marked-as-nullable)


### SynchronizeOnClassLiteralNotGetClass

Looks for code that synchronizes on the results of getClass rather than on class literals.

*   [WL: Synchronization on getClass rather than class literal (WL\_USING\_GETCLASS\_RATHER\_THAN\_CLASS\_LITERAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#wl-using-getclass-rather-than-class-literal)


### InfiniteRecursiveLoop

Looks for an infinite recursive loop.

*   [IL: A collection is added to itself (IL\_CONTAINER\_ADDED\_TO\_ITSELF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#il-container-added-to-itself)

*   [IL: An apparent infinite recursive loop (IL\_INFINITE\_RECURSIVE\_LOOP)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#il-infinite-recursive-loop)


### InfiniteLoop

Looks for an infinite loop.

*   [IL: An apparent infinite loop (IL\_INFINITE\_LOOP)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#il-infinite-loop)


### VolatileUsage

Looks for bug patterns in the usage of volatile fields.

*   [VO: An increment to a volatile field isn’t atomic (VO\_VOLATILE\_INCREMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#vo-volatile-increment)

*   [VO: A volatile reference to an array doesn’t treat the array elements as volatile (VO\_VOLATILE\_REFERENCE\_TO\_ARRAY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#vo-volatile-reference-to-array)


### InheritanceUnsafeGetResource

Looks for uses of this.getClass().getResource(...), which can give unexpected results if the class is extended by a class in another package.

*   [UI: Usage of GetResource may be unsafe if class is extended (UI\_INHERITANCE\_UNSAFE\_GETRESOURCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ui-inheritance-unsafe-getresource)


### DoInsideDoPrivileged

Looks for code that should be executed inside doPrivileged blocks.

*   [DP: Classloaders should only be created inside doPrivileged block (DP\_CREATE\_CLASSLOADER\_INSIDE\_DO\_PRIVILEGED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dp-create-classloader-inside-do-privileged)

*   [DP: Method invoked that should be only be invoked inside a doPrivileged block (DP\_DO\_INSIDE\_DO\_PRIVILEGED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dp-do-inside-do-privileged)


### HugeSharedStringConstants

This detector looks for string constants that are duplicated across multiple classfiles.

*   [HSC: Huge string constants is duplicated across multiple class files (HSC\_HUGE\_SHARED\_STRING\_CONSTANT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#hsc-huge-shared-string-constant)


### FinalizerNullsFields

This detector looks for finalizers that null out fields of a class. This does not help the garbage collector in any way, the nulling out of fields has no effect.

*   [FI: Finalizer nulls fields (FI\_FINALIZER\_NULLS\_FIELDS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fi-finalizer-nulls-fields)

*   [FI: Finalizer only nulls fields (FI\_FINALIZER\_ONLY\_NULLS\_FIELDS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fi-finalizer-only-nulls-fields)


### MutableEnum

Looks and warns about mutable enum fields.

*   [ME: Public enum method unconditionally sets its field (ME\_ENUM\_FIELD\_SETTER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#me-enum-field-setter)

*   [ME: Enum field is public and mutable (ME\_MUTABLE\_ENUM\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#me-mutable-enum-field)


### InconsistentAnnotations

This detector finds inconsistencies between type qualifiers directly applied to method parameters and uses of those method parameters.

*   [NP: Parameter must be non-null but is marked as nullable (NP\_PARAMETER\_MUST\_BE\_NONNULL\_BUT\_MARKED\_AS\_NULLABLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-parameter-must-be-nonnull-but-marked-as-nullable)


### RepeatedConditionals

This detector looks for code containing repeated conditional tests, such as (x == 5 || x == 5).

*   [RpC: Repeated conditional tests (RpC\_REPEATED\_CONDITIONAL\_TEST)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rpc-repeated-conditional-test)


### RedundantConditions

This detector looks for code containing useless conditions like the second condition in this expression: (x >= 10 && x >= 5).

*   [UC: Condition has no effect (UC\_USELESS\_CONDITION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uc-useless-condition)

*   [UC: Condition has no effect due to the variable type (UC\_USELESS\_CONDITION\_TYPE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uc-useless-condition-type)


### FormatStringChecker

Checks for incorrect format strings.

*   [FS: Format string should use %n rather than n (VA\_FORMAT\_STRING\_USES\_NEWLINE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#va-format-string-uses-newline)


### LostLoggerDueToWeakReference

This detector finds code that behaves differently under OpenJDK 6, where weak references are used to hold onto Loggers.

*   [LG: Potential lost logger changes due to weak reference in OpenJDK (LG\_LOST\_LOGGER\_DUE\_TO\_WEAK\_REFERENCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#lg-lost-logger-due-to-weak-reference)


### EqualsOperandShouldHaveClassCompatibleWithThis

Checks for equals methods that check for their operand being an instance of a class that is not compatible with the class defining the equals method.

*   [Eq: Equals checks for incompatible operand (EQ\_CHECK\_FOR\_OPERAND\_NOT\_COMPATIBLE\_WITH\_THIS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-check-for-operand-not-compatible-with-this)


### CheckImmutableAnnotation

Looks for violations of the rules for classes annotated as net.jcip.annotations.Immutable or javax.annotation.concurrent.Immutable.

*   [JCIP: Fields of immutable classes should be final (JCIP\_FIELD\_ISNT\_FINAL\_IN\_IMMUTABLE\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#jcip-field-isnt-final-in-immutable-class)


### DontCatchIllegalMonitorStateException

This detector looks for try-catch blocks that catch an IllegalMonitorStateException.

*   [IMSE: Dubious catching of IllegalMonitorStateException (IMSE\_DONT\_CATCH\_IMSE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#imse-dont-catch-imse)


### CloneIdiom

This detector looks for violations of the idioms for writing cloneable classes.

*   [CN: Class implements Cloneable but does not define or use clone method (CN\_IDIOM)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#cn-idiom)

*   [CN: clone method does not call super.clone() (CN\_IDIOM\_NO\_SUPER\_CALL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#cn-idiom-no-super-call)

*   [CN: Class defines clone() but doesn’t implement Cloneable (CN\_IMPLEMENTS\_CLONE\_BUT\_NOT\_CLONEABLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#cn-implements-clone-but-not-cloneable)


### ComparatorIdiom

This detector looks for violations of the idioms for writing classes that implement `Comparator`.

*   [Se: Comparator doesn’t implement Serializable (SE\_COMPARATOR\_SHOULD\_BE\_SERIALIZABLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-comparator-should-be-serializable)


### FindFieldSelfAssignment

This detector looks for places where a field is assigned by reading the value of the same field.

*   [SA: Self assignment of field (SA\_FIELD\_SELF\_ASSIGNMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-field-self-assignment)

*   [SA: Double assignment of local variable (SA\_LOCAL\_DOUBLE\_ASSIGNMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-local-double-assignment)


### FindSelfComparison

This detector looks for places where a value is compared with itself.

*   [SA: Double assignment of field (SA\_FIELD\_DOUBLE\_ASSIGNMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-field-double-assignment)

*   [SA: Self comparison of field with itself (SA\_FIELD\_SELF\_COMPARISON)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-field-self-comparison)

*   [SA: Nonsensical self computation involving a field (e.g., x & x) (SA\_FIELD\_SELF\_COMPUTATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-field-self-computation)

*   [SA: Self comparison of value with itself (SA\_LOCAL\_SELF\_COMPARISON)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-local-self-comparison)

*   [SA: Nonsensical self computation involving a variable (e.g., x & x) (SA\_LOCAL\_SELF\_COMPUTATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-local-self-computation)


### FindSelfComparison2

This detector looks for places where a value is compared with itself.

*   [SA: Self comparison of field with itself (SA\_FIELD\_SELF\_COMPARISON)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-field-self-comparison)

*   [SA: Nonsensical self computation involving a field (e.g., x & x) (SA\_FIELD\_SELF\_COMPUTATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-field-self-computation)

*   [SA: Self comparison of value with itself (SA\_LOCAL\_SELF\_COMPARISON)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-local-self-comparison)

*   [SA: Nonsensical self computation involving a variable (e.g., x & x) (SA\_LOCAL\_SELF\_COMPUTATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-local-self-computation)


### DroppedException

This detector looks for code where an exception is caught, but nothing is done to handle the exception.

*   [DE: Method might drop exception (DE\_MIGHT\_DROP)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#de-might-drop)

*   [DE: Method might ignore exception (DE\_MIGHT\_IGNORE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#de-might-ignore)


### LoadOfKnownNullValue

Looks for loads of values known to be null.

*   [NP: Load of known null value (NP\_LOAD\_OF\_KNOWN\_NULL\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-load-of-known-null-value)


### DumbMethodInvocations

This detector looks for bad arguments being passed to methods (e.g., substring(0)).

*   [Dm: Hardcoded constant database password (DMI\_CONSTANT\_DB\_PASSWORD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-constant-db-password)

*   [Dm: Empty database password (DMI\_EMPTY\_DB\_PASSWORD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-empty-db-password)

*   [DMI: Code contains a hard coded reference to an absolute pathname (DMI\_HARDCODED\_ABSOLUTE\_FILENAME)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-hardcoded-absolute-filename)

*   [DMI: Invocation of substring(0), which returns the original value (DMI\_USELESS\_SUBSTRING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-useless-substring)


### URLProblems

The equals and hashCode method on `java.net.URL` resolve the domain name. As a result, these operations can be very expensive, and this detector looks for places where those methods might be invoked.

*   [Dm: The equals and hashCode methods of URL are blocking (DMI\_BLOCKING\_METHODS\_ON\_URL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-blocking-methods-on-url)

*   [Dm: Maps and sets of URLs can be performance hogs (DMI\_COLLECTION\_OF\_URLS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-collection-of-urls)


### DumbMethods

This detector looks for calls to pointless methods, such as the no-argument String constructor.

*   [BC: Equals method should not assume anything about the type of its argument (BC\_EQUALS\_METHOD\_SHOULD\_WORK\_FOR\_ALL\_OBJECTS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-equals-method-should-work-for-all-objects)

*   [BIT: Bitwise add of signed byte value (BIT\_ADD\_OF\_SIGNED\_BYTE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bit-add-of-signed-byte)

*   [BIT: Bitwise OR of signed byte value (BIT\_IOR\_OF\_SIGNED\_BYTE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bit-ior-of-signed-byte)

*   [Dm: Cannot use reflection to check for presence of annotation without runtime retention (DMI\_ANNOTATION\_IS\_NOT\_VISIBLE\_TO\_REFLECTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-annotation-is-not-visible-to-reflection)

*   [DMI: Reversed method arguments (DMI\_ARGUMENTS\_WRONG\_ORDER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-arguments-wrong-order)

*   [DMI: BigDecimal constructed from double that isn’t represented precisely (DMI\_BIGDECIMAL\_CONSTRUCTED\_FROM\_DOUBLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-bigdecimal-constructed-from-double)

*   [DMI: hasNext method invokes next (DMI\_CALLING\_NEXT\_FROM\_HASNEXT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-calling-next-from-hasnext)

*   [Dm: Maps and sets of URLs can be performance hogs (DMI\_COLLECTION\_OF\_URLS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-collection-of-urls)

*   [DMI: D’oh! A nonsensical method invocation (DMI\_DOH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-doh)

*   [Dm: Futile attempt to change max pool size of ScheduledThreadPoolExecutor (DMI\_FUTILE\_ATTEMPT\_TO\_CHANGE\_MAXPOOL\_SIZE\_OF\_SCHEDULED\_THREAD\_POOL\_EXECUTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-futile-attempt-to-change-maxpool-size-of-scheduled-thread-pool-executor)

*   [DMI: Double.longBitsToDouble invoked on an int (DMI\_LONG\_BITS\_TO\_DOUBLE\_INVOKED\_ON\_INT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-long-bits-to-double-invoked-on-int)

*   [DMI: Random object created and used only once (DMI\_RANDOM\_USED\_ONLY\_ONCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-random-used-only-once)

*   [Dm: Creation of ScheduledThreadPoolExecutor with zero core threads (DMI\_SCHEDULED\_THREAD\_POOL\_EXECUTOR\_WITH\_ZERO\_CORE\_THREADS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-scheduled-thread-pool-executor-with-zero-core-threads)

*   [Dm: Thread passed where Runnable expected (DMI\_THREAD\_PASSED\_WHERE\_RUNNABLE\_EXPECTED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-thread-passed-where-runnable-expected)

*   [Dm: Useless/vacuous call to EasyMock method (DMI\_VACUOUS\_CALL\_TO\_EASYMOCK\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-vacuous-call-to-easymock-method)

*   [Dm: Method invokes inefficient Boolean constructor; use Boolean.valueOf(…) instead (DM\_BOOLEAN\_CTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-boolean-ctor)

*   [Bx: Boxing a primitive to compare (DM\_BOXED\_PRIMITIVE\_FOR\_COMPARE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-boxed-primitive-for-compare)

*   [Bx: Boxing/unboxing to parse a primitive (DM\_BOXED\_PRIMITIVE\_FOR\_PARSING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-boxed-primitive-for-parsing)

*   [Bx: Method allocates a boxed primitive just to call toString (DM\_BOXED\_PRIMITIVE\_TOSTRING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-boxed-primitive-tostring)

*   [Dm: Consider using Locale parameterized version of invoked method (DM\_CONVERT\_CASE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-convert-case)

*   [Dm: Method invokes System.exit(…) (DM\_EXIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-exit)

*   [Dm: Explicit garbage collection; extremely dubious except in benchmarking code (DM\_GC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-gc)

*   [Dm: Incorrect combination of Math.max and Math.min (DM\_INVALID\_MIN\_MAX)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-invalid-min-max)

*   [Dm: Monitor wait() called on Condition (DM\_MONITOR\_WAIT\_ON\_CONDITION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-monitor-wait-on-condition)

*   [Dm: Method allocates an object, only to get the class object (DM\_NEW\_FOR\_GETCLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-new-for-getclass)

*   [Dm: Use the nextInt method of Random rather than nextDouble to generate a random integer (DM\_NEXTINT\_VIA\_NEXTDOUBLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-nextint-via-nextdouble)

*   [Dm: Method invokes dangerous method runFinalizersOnExit (DM\_RUN\_FINALIZERS\_ON\_EXIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-run-finalizers-on-exit)

*   [Dm: Method invokes inefficient new String(String) constructor (DM\_STRING\_CTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-string-ctor)

*   [Dm: Method invokes toString() method on a String (DM\_STRING\_TOSTRING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-string-tostring)

*   [Dm: Method invokes inefficient new String() constructor (DM\_STRING\_VOID\_CTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-string-void-ctor)

*   [Dm: A thread was created using the default empty run method (DM\_USELESS\_THREAD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-useless-thread)

*   [INT: Bad comparison of int value with long constant (INT\_BAD\_COMPARISON\_WITH\_INT\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#int-bad-comparison-with-int-value)

*   [INT: Bad comparison of nonnegative value with negative constant or zero (INT\_BAD\_COMPARISON\_WITH\_NONNEGATIVE\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#int-bad-comparison-with-nonnegative-value)

*   [INT: Bad comparison of signed byte (INT\_BAD\_COMPARISON\_WITH\_SIGNED\_BYTE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#int-bad-comparison-with-signed-byte)

*   [INT: Integer remainder modulo 1 (INT\_BAD\_REM\_BY\_1)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#int-bad-rem-by-1)

*   [INT: Vacuous bit mask operation on integer value (INT\_VACUOUS\_BIT\_OPERATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#int-vacuous-bit-operation)

*   [INT: Vacuous comparison of integer value (INT\_VACUOUS\_COMPARISON)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#int-vacuous-comparison)

*   [NP: Immediate dereference of the result of readLine() (NP\_IMMEDIATE\_DEREFERENCE\_OF\_READLINE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-immediate-dereference-of-readline)

*   [RANGE: Array index is out of bounds (RANGE\_ARRAY\_INDEX)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#range-array-index)

*   [RANGE: Array length is out of bounds (RANGE\_ARRAY\_LENGTH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#range-array-length)

*   [RANGE: Array offset is out of bounds (RANGE\_ARRAY\_OFFSET)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#range-array-offset)

*   [RANGE: String index is out of bounds (RANGE\_STRING\_INDEX)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#range-string-index)

*   [RV: Random value from 0 to 1 is coerced to the integer 0 (RV\_01\_TO\_INT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-01-to-int)

*   [RV: Bad attempt to compute absolute value of signed 32-bit hashcode (RV\_ABSOLUTE\_VALUE\_OF\_HASHCODE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-absolute-value-of-hashcode)

*   [RV: Bad attempt to compute absolute value of signed random integer (RV\_ABSOLUTE\_VALUE\_OF\_RANDOM\_INT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-absolute-value-of-random-int)

*   [RV: Remainder of hashCode could be negative (RV\_REM\_OF\_HASHCODE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-rem-of-hashcode)

*   [RV: Remainder of 32-bit signed random integer (RV\_REM\_OF\_RANDOM\_INT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-rem-of-random-int)

*   [SW: Certain swing methods need to be invoked in Swing thread (SW\_SWING\_METHODS\_INVOKED\_IN\_SWING\_THREAD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sw-swing-methods-invoked-in-swing-thread)


### NumberConstructor

Looks for calls to Number constructors with primitive arguments.

*   [Bx: Method invokes inefficient floating-point Number constructor; use static valueOf instead (DM\_FP\_NUMBER\_CTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-fp-number-ctor)

*   [Bx: Method invokes inefficient Number constructor; use static valueOf instead (DM\_NUMBER\_CTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-number-ctor)


### FindSqlInjection

This detector uses data flow analysis to look for invocations of execute methods on SQL statements in which something other than a constant string is passed as an argument.

*   [SQL: Nonconstant string passed to execute or addBatch method on an SQL statement (SQL\_NONCONSTANT\_STRING\_PASSED\_TO\_EXECUTE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sql-nonconstant-string-passed-to-execute)

*   [SQL: A prepared statement is generated from a nonconstant String (SQL\_PREPARED\_STATEMENT\_GENERATED\_FROM\_NONCONSTANT\_STRING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sql-prepared-statement-generated-from-nonconstant-string)


### FindDoubleCheck

This detector looks for instances of double-checked locking.

*   [DC: Possible double-check of field (DC\_DOUBLECHECK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dc-doublecheck)

*   [DC: Possible exposure of partially initialized object (DC\_PARTIALLY\_CONSTRUCTED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dc-partially-constructed)


### FindFinalizeInvocations

This detector looks for calls to finalize() and other finalizer-related issues.

*   [FI: Empty finalizer should be deleted (FI\_EMPTY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fi-empty)

*   [FI: Explicit invocation of finalizer (FI\_EXPLICIT\_INVOCATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fi-explicit-invocation)

*   [FI: Finalizer does not call superclass finalizer (FI\_MISSING\_SUPER\_CALL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fi-missing-super-call)

*   [FI: Finalizer nullifies superclass finalizer (FI\_NULLIFY\_SUPER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fi-nullify-super)

*   [FI: Finalizer should be protected, not public (FI\_PUBLIC\_SHOULD\_BE\_PROTECTED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fi-public-should-be-protected)

*   [FI: Finalizer does nothing but call superclass finalizer (FI\_USELESS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fi-useless)


### FindHEmismatch

This detector looks for problems in the definition of the hashCode() and equals() methods.

*   [Co: Abstract class defines covariant compareTo() method (CO\_ABSTRACT\_SELF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#co-abstract-self)

*   [Co: Covariant compareTo() method defined (CO\_SELF\_NO\_OBJECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#co-self-no-object)

*   [Eq: Abstract class defines covariant equals() method (EQ\_ABSTRACT\_SELF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-abstract-self)

*   [Eq: Class defines compareTo(…) and uses Object.equals() (EQ\_COMPARETO\_USE\_OBJECT\_EQUALS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-compareto-use-object-equals)

*   [Eq: Class doesn’t override equals in superclass (EQ\_DOESNT\_OVERRIDE\_EQUALS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-doesnt-override-equals)

*   [Eq: Covariant equals() method defined for enum (EQ\_DONT\_DEFINE\_EQUALS\_FOR\_ENUM)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-dont-define-equals-for-enum)

*   [Eq: equals() method defined that doesn’t override equals(Object) (EQ\_OTHER\_NO\_OBJECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-other-no-object)

*   [Eq: equals() method defined that doesn’t override Object.equals(Object) (EQ\_OTHER\_USE\_OBJECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-other-use-object)

*   [Eq: Covariant equals() method defined (EQ\_SELF\_NO\_OBJECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-self-no-object)

*   [Eq: Covariant equals() method defined, Object.equals(Object) inherited (EQ\_SELF\_USE\_OBJECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-self-use-object)

*   [HE: Class defines equals() but not hashCode() (HE\_EQUALS\_NO\_HASHCODE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#he-equals-no-hashcode)

*   [HE: Class defines equals() and uses Object.hashCode() (HE\_EQUALS\_USE\_HASHCODE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#he-equals-use-hashcode)

*   [HE: Class defines hashCode() but not equals() (HE\_HASHCODE\_NO\_EQUALS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#he-hashcode-no-equals)

*   [HE: Class defines hashCode() and uses Object.equals() (HE\_HASHCODE\_USE\_OBJECT\_EQUALS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#he-hashcode-use-object-equals)

*   [HE: Class inherits equals() and uses Object.hashCode() (HE\_INHERITS\_EQUALS\_USE\_HASHCODE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#he-inherits-equals-use-hashcode)

*   [HE: Signature declares use of unhashable class in hashed construct (HE\_SIGNATURE\_DECLARES\_HASHING\_OF\_UNHASHABLE\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#he-signature-declares-hashing-of-unhashable-class)

*   [HE: Use of class without a hashCode() method in a hashed data structure (HE\_USE\_OF\_UNHASHABLE\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#he-use-of-unhashable-class)


### OverridingEqualsNotSymmetrical

Looks for equals methods that override equals methods in a superclass where the equivalence relationship might not be symmetrical.

*   [Eq: equals method always returns false (EQ\_ALWAYS\_FALSE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-always-false)

*   [Eq: equals method always returns true (EQ\_ALWAYS\_TRUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-always-true)

*   [Eq: equals method compares class names rather than class objects (EQ\_COMPARING\_CLASS\_NAMES)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-comparing-class-names)

*   [Eq: equals method fails for subtypes (EQ\_GETCLASS\_AND\_CLASS\_CONSTANT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-getclass-and-class-constant)

*   [Eq: equals method overrides equals in superclass and may not be symmetric (EQ\_OVERRIDING\_EQUALS\_NOT\_SYMMETRIC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-overriding-equals-not-symmetric)

*   [Eq: Unusual equals method (EQ\_UNUSUAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eq-unusual)


### FindNakedNotify

This detector looks for calls to notify() that don't seem to modify mutable object state.

*   [NN: Naked notify (NN\_NAKED\_NOTIFY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nn-naked-notify)


### FindReturnRef

This detector looks for methods that return mutable static data.

*   [EI: May expose internal representation by returning a buffer sharing non-public data (EI\_EXPOSE\_BUF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ei-expose-buf)

*   [EI2: May expose internal representation by creating a buffer which incorporates reference to array (EI\_EXPOSE\_BUF2)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ei-expose-buf2)

*   [EI: May expose internal representation by returning reference to mutable object (EI\_EXPOSE\_REP)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ei-expose-rep)

*   [EI2: May expose internal representation by incorporating reference to mutable object (EI\_EXPOSE\_REP2)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ei-expose-rep2)

*   [MS: May expose internal static state by creating a buffer which stores an external array into a static field (EI\_EXPOSE\_STATIC\_BUF2)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ei-expose-static-buf2)

*   [MS: May expose internal static state by storing a mutable object into a static field (EI\_EXPOSE\_STATIC\_REP2)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ei-expose-static-rep2)

*   [MS: May expose internal representation by returning a buffer sharing non-public data (MS\_EXPOSE\_BUF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-expose-buf)

*   [MS: Public static method may expose internal representation by returning a mutable object or array (MS\_EXPOSE\_REP)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-expose-rep)


### FindRunInvocations

This detector looks for calls to Thread.run(). It is a fast detector.

*   [Ru: Invokes run on a thread (did you mean to start it instead?) (RU\_INVOKE\_RUN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ru-invoke-run)


### SwitchFallthrough

This detector looks for switch statements containing fall through.

*   [SF: Dead store due to switch statement fall through (SF\_DEAD\_STORE\_DUE\_TO\_SWITCH\_FALLTHROUGH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sf-dead-store-due-to-switch-fallthrough)

*   [SF: Dead store due to switch statement fall through to throw (SF\_DEAD\_STORE\_DUE\_TO\_SWITCH\_FALLTHROUGH\_TO\_THROW)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sf-dead-store-due-to-switch-fallthrough-to-throw)

*   [SF: Switch statement found where one case falls through to the next case (SF\_SWITCH\_FALLTHROUGH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sf-switch-fallthrough)

*   [SF: Switch statement found where default case is missing (SF\_SWITCH\_NO\_DEFAULT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sf-switch-no-default)


### FindSpinLoop

This detector looks for loops that spin reading from a field.

*   [SP: Method spins on field (SP\_SPIN\_ON\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sp-spin-on-field)


### FindNonShortCircuit

This detector looks for suspicious uses of non-short-circuiting boolean operators (`|` and `&` instead of `||` and `&&`).

*   [NS: Potentially dangerous use of non-short-circuit logic (NS\_DANGEROUS\_NON\_SHORT\_CIRCUIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ns-dangerous-non-short-circuit)

*   [NS: Questionable use of non-short-circuit logic (NS\_NON\_SHORT\_CIRCUIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ns-non-short-circuit)


### FindTwoLockWait

This detector looks for calls to wait() with two (or more) locks held. It is a slow detector.

*   [TLW: Wait with two locks held (TLW\_TWO\_LOCK\_WAIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tlw-two-lock-wait)


### FindUnconditionalWait

This detector looks for calls to wait() not in a conditional or loop.

*   [UW: Unconditional wait (UW\_UNCOND\_WAIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uw-uncond-wait)


### FindUninitializedGet

This detector looks for reads of uninitialized fields in constructors.

*   [UR: Uninitialized read of field in constructor (UR\_UNINIT\_READ)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ur-uninit-read)


### DontUseEnum

Checks that fields and methods don't use the name assert or enum as they are keywords in Java 5.

*   [Nm: Use of identifier that is a keyword in later versions of Java (NM\_FUTURE\_KEYWORD\_USED\_AS\_IDENTIFIER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-future-keyword-used-as-identifier)

*   [Nm: Use of identifier that is a keyword in later versions of Java (NM\_FUTURE\_KEYWORD\_USED\_AS\_MEMBER\_IDENTIFIER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-future-keyword-used-as-member-identifier)


### FindUnsyncGet

This detector looks for get and set methods where the get is unsynchronized while the set is synchronized.

*   [UG: Unsynchronized get method, synchronized set method (UG\_SYNC\_SET\_UNSYNC\_GET)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ug-sync-set-unsync-get)


### InitializationChain

This detector looks for potentially circular class initialization dependencies.

*   [IC: Initialization circularity (IC\_INIT\_CIRCULARITY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ic-init-circularity)

*   [SI: Static initializer creates instance before all static final fields assigned (SI\_INSTANCE\_BEFORE\_FINALS\_ASSIGNED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#si-instance-before-finals-assigned)


### IteratorIdioms

This detector looks for problems in how Iterator classes are defined.

*   [It: Iterator next() method cannot throw NoSuchElementException (IT\_NO\_SUCH\_ELEMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#it-no-such-element)


### PreferZeroLengthArrays

This detector looks for methods that return either arrays or an explicit null reference. Returning a zero length array is generally preferred in this context to returning a null reference.

*   [PZLA: Consider returning a zero length array rather than null (PZLA\_PREFER\_ZERO\_LENGTH\_ARRAYS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#pzla-prefer-zero-length-arrays)


### SynchronizingOnContentsOfFieldToProtectField

This detector looks for code that seems to be synchronizing on a field in order to guard updates of that field.

*   [ML: Synchronization on field in futile attempt to guard that field (ML\_SYNC\_ON\_FIELD\_TO\_GUARD\_CHANGING\_THAT\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ml-sync-on-field-to-guard-changing-that-field)


### MutableLock

This detector looks for synchronization on objects read from modified fields.

*   [ML: Method synchronizes on an updated field (ML\_SYNC\_ON\_UPDATED\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ml-sync-on-updated-field)


### FindUselessObjects

Looks for useless objects.

*   [UC: Useless object created (UC\_USELESS\_OBJECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uc-useless-object)

*   [UC: Useless object created on stack (UC\_USELESS\_OBJECT\_STACK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uc-useless-object-stack)


### MutableStaticFields

This detector looks for static fields that may be modified by malicious code.

*   [MS: Field isn’t final and cannot be protected from malicious code (MS\_CANNOT\_BE\_FINAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-cannot-be-final)

*   [MS: Field should be both final and package protected (MS\_FINAL\_PKGPROTECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-final-pkgprotect)

*   [MS: Field is a mutable array (MS\_MUTABLE\_ARRAY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-mutable-array)

*   [MS: Field is a mutable collection (MS\_MUTABLE\_COLLECTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-mutable-collection)

*   [MS: Field is a mutable collection which should be package protected (MS\_MUTABLE\_COLLECTION\_PKGPROTECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-mutable-collection-pkgprotect)

*   [MS: Field is a mutable Hashtable (MS\_MUTABLE\_HASHTABLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-mutable-hashtable)

*   [MS: Field should be moved out of an interface and made package protected (MS\_OOI\_PKGPROTECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-ooi-pkgprotect)

*   [MS: Field should be package protected (MS\_PKGPROTECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-pkgprotect)

*   [MS: Field isn’t final but should be (MS\_SHOULD\_BE\_FINAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-should-be-final)

*   [MS: Field isn’t final but should be refactored to be so (MS\_SHOULD\_BE\_REFACTORED\_TO\_BE\_FINAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ms-should-be-refactored-to-be-final)


### Naming

This detector looks for suspiciously-named methods.

*   [Nm: Class defines equal(Object); should it be equals(Object)? (NM\_BAD\_EQUAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-bad-equal)

*   [Nm: Class names should start with an upper case letter (NM\_CLASS\_NAMING\_CONVENTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-class-naming-convention)

*   [Nm: Class is not derived from an Exception, even though it is named as such (NM\_CLASS\_NOT\_EXCEPTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-class-not-exception)

*   [Nm: Confusing method names (NM\_CONFUSING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-confusing)

*   [Nm: Non-final field names should start with a lower case letter, final fields should be uppercase with words separated by underscores (NM\_FIELD\_NAMING\_CONVENTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-field-naming-convention)

*   [Nm: Class defines hashcode(); should it be hashCode()? (NM\_LCASE\_HASHCODE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-lcase-hashcode)

*   [Nm: Class defines tostring(); should it be toString()? (NM\_LCASE\_TOSTRING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-lcase-tostring)

*   [Nm: Apparent method/constructor confusion (NM\_METHOD\_CONSTRUCTOR\_CONFUSION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-method-constructor-confusion)

*   [Nm: Method names should start with a lower case letter (NM\_METHOD\_NAMING\_CONVENTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-method-naming-convention)

*   [Nm: Class names shouldn’t shadow simple name of implemented interface (NM\_SAME\_SIMPLE\_NAME\_AS\_INTERFACE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-same-simple-name-as-interface)

*   [Nm: Class names shouldn’t shadow simple name of superclass (NM\_SAME\_SIMPLE\_NAME\_AS\_SUPERCLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-same-simple-name-as-superclass)

*   [Nm: Very confusing method names (NM\_VERY\_CONFUSING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-very-confusing)

*   [Nm: Very confusing method names (but perhaps intentional) (NM\_VERY\_CONFUSING\_INTENTIONAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-very-confusing-intentional)

*   [Nm: Method doesn’t override method in superclass due to wrong package for parameter (NM\_WRONG\_PACKAGE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-wrong-package)

*   [Nm: Method doesn’t override method in superclass due to wrong package for parameter (NM\_WRONG\_PACKAGE\_INTENTIONAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#nm-wrong-package-intentional)


### ReadReturnShouldBeChecked

This detector looks for calls to InputStream.read() or InputStream.skip() where the return value is ignored.

*   [RR: Method ignores results of InputStream.read() (RR\_NOT\_CHECKED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rr-not-checked)

*   [RR: Method ignores results of InputStream.skip() (SR\_NOT\_CHECKED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sr-not-checked)


### SerializableIdiom

This detector looks for potential problems in the implementation of Serializable classes.

*   [RS: Class’s readObject() method is synchronized (RS\_READOBJECT\_SYNC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rs-readobject-sync)

*   [Se: Non-transient non-serializable instance field in serializable class (SE\_BAD\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-bad-field)

*   [Se: Non-serializable class has a serializable inner class (SE\_BAD\_FIELD\_INNER\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-bad-field-inner-class)

*   [Se: Non-serializable value stored into instance field of a serializable class (SE\_BAD\_FIELD\_STORE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-bad-field-store)

*   [Se: Serializable inner class (SE\_INNER\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-inner-class)

*   [Se: Method must be private in order for serialization to work (SE\_METHOD\_MUST\_BE\_PRIVATE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-method-must-be-private)

*   [Se: serialVersionUID isn’t final (SE\_NONFINAL\_SERIALVERSIONID)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-nonfinal-serialversionid)

*   [Se: serialVersionUID isn’t long (SE\_NONLONG\_SERIALVERSIONID)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-nonlong-serialversionid)

*   [Se: serialVersionUID isn’t static (SE\_NONSTATIC\_SERIALVERSIONID)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-nonstatic-serialversionid)

*   [SnVI: Class is Serializable, but doesn’t define serialVersionUID (SE\_NO\_SERIALVERSIONID)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-no-serialversionid)

*   [Se: Class is Serializable but its superclass doesn’t define a void constructor (SE\_NO\_SUITABLE\_CONSTRUCTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-no-suitable-constructor)

*   [Se: Class is Externalizable but doesn’t define a void constructor (SE\_NO\_SUITABLE\_CONSTRUCTOR\_FOR\_EXTERNALIZATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-no-suitable-constructor-for-externalization)

*   [Se: Prevent overwriting of externalizable objects (SE\_PREVENT\_EXT\_OBJ\_OVERWRITE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-prevent-ext-obj-overwrite)

*   [Se: Private readResolve method not inherited by subclasses (SE\_PRIVATE\_READ\_RESOLVE\_NOT\_INHERITED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-private-read-resolve-not-inherited)

*   [Se: The readResolve method must not be declared as a static method. (SE\_READ\_RESOLVE\_IS\_STATIC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-read-resolve-is-static)

*   [Se: The readResolve method must be declared with a return type of Object. (SE\_READ\_RESOLVE\_MUST\_RETURN\_OBJECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-read-resolve-must-return-object)

*   [Se: Transient field that isn’t set by deserialization. (SE\_TRANSIENT\_FIELD\_NOT\_RESTORED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-transient-field-not-restored)

*   [Se: Transient field of class that isn’t Serializable. (SE\_TRANSIENT\_FIELD\_OF\_NONSERIALIZABLE\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#se-transient-field-of-nonserializable-class)

*   [WS: Class’s writeObject() method is synchronized but nothing else is (WS\_WRITEOBJECT\_SYNC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ws-writeobject-sync)


### StartInConstructor

This detector looks for constructors that start threads.

*   [SC: Constructor invokes Thread.start() (SC\_START\_IN\_CTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sc-start-in-ctor)


### FindBadForLoop

This detector looks for incorrect for loops.

*   [QF: Complicated, subtle or wrong increment in for-loop (QF\_QUESTIONABLE\_FOR\_LOOP)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#qf-questionable-for-loop)


### ExplicitSerialization

Looks for explicit serialization via readObject and writeObject as evidence that this class is, indeed, serialized.

*   :ref:\`\`


### UnreadFields

This detector looks for fields whose value is never read.

*   [NP: Read of unwritten field (NP\_UNWRITTEN\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-unwritten-field)

*   [NP: Read of unwritten public or protected field (NP\_UNWRITTEN\_PUBLIC\_OR\_PROTECTED\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-unwritten-public-or-protected-field)

*   [SIC: Should be a static inner class (SIC\_INNER\_SHOULD\_BE\_STATIC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sic-inner-should-be-static)

*   [SIC: Could be refactored into a named static inner class (SIC\_INNER\_SHOULD\_BE\_STATIC\_ANON)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sic-inner-should-be-static-anon)

*   [SIC: Could be refactored into a static inner class (SIC\_INNER\_SHOULD\_BE\_STATIC\_NEEDS\_THIS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sic-inner-should-be-static-needs-this)

*   [SIC: Deadly embrace of non-static inner class and thread local (SIC\_THREADLOCAL\_DEADLY\_EMBRACE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sic-threadlocal-deadly-embrace)

*   [SS: Unread field: should this field be static? (SS\_SHOULD\_BE\_STATIC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ss-should-be-static)

*   [ST: Write to static field from instance method (ST\_WRITE\_TO\_STATIC\_FROM\_INSTANCE\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#st-write-to-static-from-instance-method)

*   [UrF: Unread field (URF\_UNREAD\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#urf-unread-field)

*   [UrF: Unread public/protected field (URF\_UNREAD\_PUBLIC\_OR\_PROTECTED\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#urf-unread-public-or-protected-field)

*   [UuF: Unused field (UUF\_UNUSED\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uuf-unused-field)

*   [UuF: Unused public or protected field (UUF\_UNUSED\_PUBLIC\_OR\_PROTECTED\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uuf-unused-public-or-protected-field)

*   [UwF: Field not initialized in constructor but dereferenced without null check (UWF\_FIELD\_NOT\_INITIALIZED\_IN\_CONSTRUCTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uwf-field-not-initialized-in-constructor)

*   [UwF: Field only ever set to null (UWF\_NULL\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uwf-null-field)

*   [UwF: Unwritten field (UWF\_UNWRITTEN\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uwf-unwritten-field)

*   [UwF: Unwritten public or protected field (UWF\_UNWRITTEN\_PUBLIC\_OR\_PROTECTED\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uwf-unwritten-public-or-protected-field)


### WaitInLoop

This detector looks for calls to wait() that are not in a loop.

*   [No: Using notify() rather than notifyAll() (NO\_NOTIFY\_NOT\_NOTIFYALL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#no-notify-not-notifyall)

*   [Wa: Condition.await() not in loop (WA\_AWAIT\_NOT\_IN\_LOOP)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#wa-await-not-in-loop)

*   [Wa: Wait not in loop (WA\_NOT\_IN\_LOOP)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#wa-not-in-loop)


### FindComparatorProblems

This detector looks for problems in Comparator.compare or Comparable.compareTo implementation.

*   [Co: compareTo()/compare() incorrectly handles float or double value (CO\_COMPARETO\_INCORRECT\_FLOATING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#co-compareto-incorrect-floating)

*   [Co: compareTo()/compare() returns Integer.MIN\_VALUE (CO\_COMPARETO\_RESULTS\_MIN\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#co-compareto-results-min-value)


### FindNullDeref

This detector looks for places where a null pointer exception might occur. It also looks for redundant comparisons of reference values against null. It is a slow detector.

*   [NP: Null pointer dereference (NP\_ALWAYS\_NULL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-always-null)

*   [NP: Null pointer dereference in method on exception path (NP\_ALWAYS\_NULL\_EXCEPTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-always-null-exception)

*   [NP: Method does not check for null argument (NP\_ARGUMENT\_MIGHT\_BE\_NULL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-argument-might-be-null)

*   [NP: Clone method may return null (NP\_CLONE\_COULD\_RETURN\_NULL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-clone-could-return-null)

*   [NP: close() invoked on a value that is always null (NP\_CLOSING\_NULL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-closing-null)

*   [NP: Dereference of the result of readLine() without nullcheck (NP\_DEREFERENCE\_OF\_READLINE\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-dereference-of-readline-value)

*   [NP: equals() method does not check for null argument (NP\_EQUALS\_SHOULD\_HANDLE\_NULL\_ARGUMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-equals-should-handle-null-argument)

*   [NP: Null value is guaranteed to be dereferenced (NP\_GUARANTEED\_DEREF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-guaranteed-deref)

*   [NP: Value is null and guaranteed to be dereferenced on exception path (NP\_GUARANTEED\_DEREF\_ON\_EXCEPTION\_PATH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-guaranteed-deref-on-exception-path)

*   [NP: Method call passes null to a non-null parameter (NP\_NONNULL\_PARAM\_VIOLATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-nonnull-param-violation)

*   [NP: Method may return null, but is declared @Nonnull (NP\_NONNULL\_RETURN\_VIOLATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-nonnull-return-violation)

*   [NP: Possible null pointer dereference (NP\_NULL\_ON\_SOME\_PATH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-on-some-path)

*   [NP: Possible null pointer dereference in method on exception path (NP\_NULL\_ON\_SOME\_PATH\_EXCEPTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-on-some-path-exception)

*   [NP: Possible null pointer dereference due to return value of called method (NP\_NULL\_ON\_SOME\_PATH\_FROM\_RETURN\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-on-some-path-from-return-value)

*   [NP: Possible null pointer dereference on branch that might be infeasible (NP\_NULL\_ON\_SOME\_PATH\_MIGHT\_BE\_INFEASIBLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-on-some-path-might-be-infeasible)

*   [NP: Method call passes null for non-null parameter (NP\_NULL\_PARAM\_DEREF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-param-deref)

*   [NP: Method call passes null for non-null parameter (NP\_NULL\_PARAM\_DEREF\_ALL\_TARGETS\_DANGEROUS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-param-deref-all-targets-dangerous)

*   [NP: Non-virtual method call passes null for non-null parameter (NP\_NULL\_PARAM\_DEREF\_NONVIRTUAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-param-deref-nonvirtual)

*   [NP: Store of null value into field annotated @Nonnull (NP\_STORE\_INTO\_NONNULL\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-store-into-nonnull-field)

*   [NP: toString method may return null (NP\_TOSTRING\_COULD\_RETURN\_NULL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-tostring-could-return-null)

*   [RCN: Redundant comparison of non-null value to null (RCN\_REDUNDANT\_COMPARISON\_OF\_NULL\_AND\_NONNULL\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rcn-redundant-comparison-of-null-and-nonnull-value)

*   [RCN: Redundant comparison of two null values (RCN\_REDUNDANT\_COMPARISON\_TWO\_NULL\_VALUES)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rcn-redundant-comparison-two-null-values)

*   [RCN: Redundant nullcheck of value known to be non-null (RCN\_REDUNDANT\_NULLCHECK\_OF\_NONNULL\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rcn-redundant-nullcheck-of-nonnull-value)

*   [RCN: Redundant nullcheck of value known to be null (RCN\_REDUNDANT\_NULLCHECK\_OF\_NULL\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rcn-redundant-nullcheck-of-null-value)

*   [RCN: Nullcheck of value previously dereferenced (RCN\_REDUNDANT\_NULLCHECK\_WOULD\_HAVE\_BEEN\_A\_NPE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rcn-redundant-nullcheck-would-have-been-a-npe)


### FindNullDerefsInvolvingNonShortCircuitEvaluation

This detector looks for places where a null pointer exception might occur, and the use of non-short-circuit evaluation causes the usual techniques to fail.

*   [NP: Null value is guaranteed to be dereferenced (NP\_GUARANTEED\_DEREF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-guaranteed-deref)

*   [NP: Possible null pointer dereference (NP\_NULL\_ON\_SOME\_PATH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-on-some-path)


### FindOpenStream

This detector looks for IO stream objects which do not escape the method and do not appear to be closed on all paths out of the method. It is a slow detector.

*   [ODR: Method may fail to close database resource (ODR\_OPEN\_DATABASE\_RESOURCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#odr-open-database-resource)

*   [ODR: Method may fail to close database resource on exception (ODR\_OPEN\_DATABASE\_RESOURCE\_EXCEPTION\_PATH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#odr-open-database-resource-exception-path)

*   [OS: Method may fail to close stream (OS\_OPEN\_STREAM)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#os-open-stream)

*   [OS: Method may fail to close stream on exception (OS\_OPEN\_STREAM\_EXCEPTION\_PATH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#os-open-stream-exception-path)


### FindUselessControlFlow

This detector looks for control flow statements which have no effect.

*   [UCF: Useless control flow (UCF\_USELESS\_CONTROL\_FLOW)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ucf-useless-control-flow)

*   [UCF: Useless control flow to next line (UCF\_USELESS\_CONTROL\_FLOW\_NEXT\_LINE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ucf-useless-control-flow-next-line)


### FindUnreleasedLock

This detector looks for JSR-166 (`java.util.concurrent`) locks which are acquired, but not released on all paths out of the method.  It is a moderately fast detector.  Note that in order to use this detector, you need to have the `java.util.concurrent` package in the auxiliary classpath (or be analyzing the package itself).

*   [UL: Method does not release lock on all paths (UL\_UNRELEASED\_LOCK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ul-unreleased-lock)

*   [UL: Method does not release lock on all exception paths (UL\_UNRELEASED\_LOCK\_EXCEPTION\_PATH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ul-unreleased-lock-exception-path)


### FindRefComparison

This detector looks for places where two reference values are compared with the == or != operator, and the class is of a type (such as `java.lang.String`) where comparing reference values is generally an error. It is a slow detector.

*   [DMI: D’oh! A nonsensical method invocation (DMI\_DOH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-doh)

*   [EC: equals() used to compare array and nonarray (EC\_ARRAY\_AND\_NONARRAY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-array-and-nonarray)

*   [EC: Invocation of equals() on an array, which is equivalent to == (EC\_BAD\_ARRAY\_COMPARE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-bad-array-compare)

*   [EC: equals(…) used to compare incompatible arrays (EC\_INCOMPATIBLE\_ARRAY\_COMPARE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-incompatible-array-compare)

*   [EC: Call to equals(null) (EC\_NULL\_ARG)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-null-arg)

*   [EC: Call to equals() comparing unrelated class and interface (EC\_UNRELATED\_CLASS\_AND\_INTERFACE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-unrelated-class-and-interface)

*   [EC: Call to equals() comparing different interface types (EC\_UNRELATED\_INTERFACES)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-unrelated-interfaces)

*   [EC: Call to equals() comparing different types (EC\_UNRELATED\_TYPES)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-unrelated-types)

*   [EC: Using pointer equality to compare different types (EC\_UNRELATED\_TYPES\_USING\_POINTER\_EQUALITY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-unrelated-types-using-pointer-equality)

*   [ES: Comparison of String parameter using == or != (ES\_COMPARING\_PARAMETER\_STRING\_WITH\_EQ)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#es-comparing-parameter-string-with-eq)

*   [ES: Comparison of String objects using == or != (ES\_COMPARING\_STRINGS\_WITH\_EQ)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#es-comparing-strings-with-eq)

*   [RC: Suspicious reference comparison (RC\_REF\_COMPARISON)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rc-ref-comparison)

*   [RC: Suspicious reference comparison to constant (RC\_REF\_COMPARISON\_BAD\_PRACTICE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rc-ref-comparison-bad-practice)

*   [RC: Suspicious reference comparison of Boolean values (RC\_REF\_COMPARISON\_BAD\_PRACTICE\_BOOLEAN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rc-ref-comparison-bad-practice-boolean)


### FindMismatchedWaitOrNotify

This detector looks for calls to wait(), notify(), or notifyAll() which do not appear to be made on an object which is currently locked.  It is a moderately fast detector.  **This detector is disabled because it is still under development, and produces too many false positives.**

*   [MWN: Mismatched notify() (MWN\_MISMATCHED\_NOTIFY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mwn-mismatched-notify)

*   [MWN: Mismatched wait() (MWN\_MISMATCHED\_WAIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mwn-mismatched-wait)


### FindEmptySynchronizedBlock

This detector looks for empty synchronized blocks.

*   [ESync: Empty synchronized block (ESync\_EMPTY\_SYNC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#esync-empty-sync)


### FindInconsistentSync2

This detector looks for fields that are accessed in an inconsistent manner with respect to locking. It is a slow detector.

*   [IS: Inconsistent synchronization (IS2\_INCONSISTENT\_SYNC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#is2-inconsistent-sync)

*   [IS: Field not guarded against concurrent access (IS\_FIELD\_NOT\_GUARDED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#is-field-not-guarded)

*   [MSF: Mutable servlet field (MSF\_MUTABLE\_SERVLET\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#msf-mutable-servlet-field)


### FindLocalSelfAssignment2

This detector looks for self assignments of local variables.

*   [SA: Self assignment of local variable (SA\_LOCAL\_SELF\_ASSIGNMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-local-self-assignment)

*   [SA: Self assignment of local rather than assignment to field (SA\_LOCAL\_SELF\_ASSIGNMENT\_INSTEAD\_OF\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sa-local-self-assignment-instead-of-field)


### IncompatMask

This detector looks for suspicious bitwise logical expressions.

*   [BIT: Incompatible bit masks (BIT\_AND)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bit-and)

*   [BIT: Check to see if ((…) & 0) == 0 (BIT\_AND\_ZZ)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bit-and-zz)

*   [BIT: Incompatible bit masks (BIT\_IOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bit-ior)

*   [BIT: Check for sign of bitwise operation (BIT\_SIGNED\_CHECK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bit-signed-check)

*   [BIT: Check for sign of bitwise operation involving negative number (BIT\_SIGNED\_CHECK\_HIGH\_BIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bit-signed-check-high-bit)


### LazyInit

This detector looks for lazy field initialization where the field is not volatile. It is a moderately fast detector.

*   [LI: Incorrect lazy initialization of static field (LI\_LAZY\_INIT\_STATIC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#li-lazy-init-static)

*   [LI: Incorrect lazy initialization and update of static field (LI\_LAZY\_INIT\_UPDATE\_STATIC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#li-lazy-init-update-static)


### FindJSR166LockMonitorenter

This detector looks for ordinary synchronization performed on JSR166 locks. It is a moderately fast detector.

*   [JLM: Synchronization performed on Lock (JLM\_JSR166\_LOCK\_MONITORENTER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#jlm-jsr166-lock-monitorenter)

*   [JLM: Synchronization performed on util.concurrent instance (JLM\_JSR166\_UTILCONCURRENT\_MONITORENTER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#jlm-jsr166-utilconcurrent-monitorenter)

*   [JLM: Using monitor style wait methods on util.concurrent abstraction (JML\_JSR166\_CALLING\_WAIT\_RATHER\_THAN\_AWAIT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#jml-jsr166-calling-wait-rather-than-await)


### FindUncalledPrivateMethods

This detector looks for private methods that are never called.

*   [UPM: Private method is never called (UPM\_UNCALLED\_PRIVATE\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#upm-uncalled-private-method)


### UncallableMethodOfAnonymousClass

This detector looks for anonymous inner classes that define methods that are probably intended to but do not override methods in a superclass.

*   [UMAC: Uncallable method defined in anonymous class (UMAC\_UNCALLABLE\_METHOD\_OF\_ANONYMOUS\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#umac-uncallable-method-of-anonymous-class)


### StringConcatenation

This detector looks for String concatenation in loops using +.

*   [SBSC: Method concatenates strings using + in a loop (SBSC\_USE\_STRINGBUFFER\_CONCATENATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sbsc-use-stringbuffer-concatenation)


### InvalidJUnitTest

This detector looks for JUnit tests that are malformed.

*   [IJU: TestCase declares a bad suite method (IJU\_BAD\_SUITE\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#iju-bad-suite-method)

*   [IJU: TestCase has no tests (IJU\_NO\_TESTS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#iju-no-tests)

*   [IJU: TestCase defines setUp that doesn’t call super.setUp() (IJU\_SETUP\_NO\_SUPER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#iju-setup-no-super)

*   [IJU: TestCase implements a non-static suite method (IJU\_SUITE\_NOT\_STATIC)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#iju-suite-not-static)

*   [IJU: TestCase defines tearDown that doesn’t call super.tearDown() (IJU\_TEARDOWN\_NO\_SUPER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#iju-teardown-no-super)


### BadlyOverriddenAdapter

This detector looks for code that extends an Adapter class and overrides a Listener method with the wrong signature.

*   [BOA: Class overrides a method implemented in super class Adapter wrongly (BOA\_BADLY\_OVERRIDDEN\_ADAPTER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#boa-badly-overridden-adapter)


### BadResultSetAccess

This detector looks for calls to getXXX or setXXX methods of a result set where the field index is 0. As ResultSet fields start at index 1, this is always a mistake.

*   [SQL: Method attempts to access a prepared statement parameter with index 0 (SQL\_BAD\_PREPARED\_STATEMENT\_ACCESS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sql-bad-prepared-statement-access)

*   [SQL: Method attempts to access a result set field with index 0 (SQL\_BAD\_RESULTSET\_ACCESS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sql-bad-resultset-access)


### SuperfluousInstanceOf

This detector looks for type checks using the instanceof operator where the determination can be done statically.

*   [SIO: Unnecessary type check done using instanceof operator (SIO\_SUPERFLUOUS\_INSTANCEOF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sio-superfluous-instanceof)


### SuspiciousThreadInterrupted

This detector looks for calls to Thread.interrupted() from a non-static context. If it is called from Thread.currentThread().interrupted(), then it is just a useless exercise, just use Thread.interrupted(). However if it is called on an arbitrary thread object, it is most probably an error, as interrupted() is always called on the current thread.

*   [STI: Unneeded use of currentThread() call, to call interrupted() (STI\_INTERRUPTED\_ON\_CURRENTTHREAD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sti-interrupted-on-currentthread)

*   [STI: Static Thread.interrupted() method invoked on thread instance (STI\_INTERRUPTED\_ON\_UNKNOWNTHREAD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sti-interrupted-on-unknownthread)


### FindDeadLocalStores

This detector looks for assignments to local variables that are never subsequently read. It is a moderately fast detector.

*   [DLS: Useless increment in return statement (DLS\_DEAD\_LOCAL\_INCREMENT\_IN\_RETURN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dls-dead-local-increment-in-return)

*   [DLS: Dead store to local variable (DLS\_DEAD\_LOCAL\_STORE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dls-dead-local-store)

*   [DLS: Dead store of null to local variable (DLS\_DEAD\_LOCAL\_STORE\_OF\_NULL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dls-dead-local-store-of-null)

*   [DLS: Dead store to local variable that shadows field (DLS\_DEAD\_LOCAL\_STORE\_SHADOWS\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dls-dead-local-store-shadows-field)

*   [DLS: Dead store of class literal (DLS\_DEAD\_STORE\_OF\_CLASS\_LITERAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dls-dead-store-of-class-literal)

*   [IP: A parameter is dead upon entry to a method but overwritten (IP\_PARAMETER\_IS\_DEAD\_BUT\_OVERWRITTEN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ip-parameter-is-dead-but-overwritten)


### FindMaskedFields

This detector looks for class level fields that are masked by local fields defined in methods.

*   [MF: Class defines field that masks a superclass field (MF\_CLASS\_MASKS\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mf-class-masks-field)

*   [MF: Method defines a variable that obscures a field (MF\_METHOD\_MASKS\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mf-method-masks-field)


### WrongMapIterator

This detector looks for accessing the value of a Map entry, using a key that was retrieved from a keySet iterator.

*   [WMI: Inefficient use of keySet iterator instead of entrySet iterator (WMI\_WRONG\_MAP\_ITERATOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#wmi-wrong-map-iterator)


### InstantiateStaticClass

This detector looks for code that creates objects based on classes that only define static methods.

*   [ISC: Needless instantiation of class that only supplies static methods (ISC\_INSTANTIATE\_STATIC\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#isc-instantiate-static-class)


### RuntimeExceptionCapture

This detector looks for catch clauses that catch Exception, when no code in the block throws Exception.

*   [REC: Exception is caught when Exception is not thrown (REC\_CATCH\_EXCEPTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rec-catch-exception)


### DontCatchNullPointerException

Nullpointer exceptions should not be caught.

*   [DCN: NullPointerException caught (DCN\_NULLPOINTER\_EXCEPTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dcn-nullpointer-exception)


### FindFloatEquality

Looks for floating point equality expressions. A fast detector.

*   [FE: Test for floating point equality (FE\_FLOATING\_POINT\_EQUALITY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fe-floating-point-equality)

*   [FE: Doomed test for equality to NaN (FE\_TEST\_IF\_EQUAL\_TO\_NOT\_A\_NUMBER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fe-test-if-equal-to-not-a-number)


### FindUnsatisfiedObligation

This detector looks for I/O streams and database resources that are not cleaned up on all paths out of a method. This is a slow detector.

*   [OBL: Method may fail to clean up stream or resource (OBL\_UNSATISFIED\_OBLIGATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#obl-unsatisfied-obligation)

*   [OBL: Method may fail to clean up stream or resource on checked exception (OBL\_UNSATISFIED\_OBLIGATION\_EXCEPTION\_EDGE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#obl-unsatisfied-obligation-exception-edge)


### UnnecessaryMath

This detector looks for code that calls java.lang.Math static methods on constant values, where the resultant value is a statically known constant. It is faster, and sometimes more accurate, to use the constant instead.

*   [UM: Method calls static Math class method on a constant value (UM\_UNNECESSARY\_MATH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#um-unnecessary-math)


### RedundantInterfaces

This detector looks for classes that declare they implement the same interface as a super class. This is redundant, if a superclass implements an interface, so does the subclass.

*   [RI: Class implements same interface as superclass (RI\_REDUNDANT\_INTERFACES)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ri-redundant-interfaces)


### MultithreadedInstanceAccess

This detector looks for potential problems in implementing the Struts framework.

*   [MTIA: Class extends Servlet class and uses instance variables (MTIA\_SUSPECT\_SERVLET\_INSTANCE\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mtia-suspect-servlet-instance-field)

*   [MTIA: Class extends Struts Action class and uses instance variables (MTIA\_SUSPECT\_STRUTS\_INSTANCE\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mtia-suspect-struts-instance-field)


### BadUseOfReturnValue

Looks for cases where the return value of a function is discarded after being checked for non-null.

*   [RV: Method checks to see if result of String.indexOf is positive (RV\_CHECK\_FOR\_POSITIVE\_INDEXOF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-check-for-positive-indexof)

*   [RV: Method discards result of readLine after checking if it is non-null (RV\_DONT\_JUST\_NULL\_CHECK\_READLINE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-dont-just-null-check-readline)


### MethodReturnCheck

This detector looks for calls to methods where the return value is suspiciously ignored.

*   [RV: Code checks for specific values returned by compareTo (RV\_CHECK\_COMPARETO\_FOR\_SPECIFIC\_RETURN\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-check-compareto-for-specific-return-value)

*   [RV: Exception created and dropped rather than thrown (RV\_EXCEPTION\_NOT\_THROWN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-exception-not-thrown)

*   [RV: Method ignores return value (RV\_RETURN\_VALUE\_IGNORED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-return-value-ignored)

*   [RV: Method ignores exceptional return value (RV\_RETURN\_VALUE\_IGNORED\_BAD\_PRACTICE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-return-value-ignored-bad-practice)

*   [RV: Method ignores return value, is this OK? (RV\_RETURN\_VALUE\_IGNORED\_INFERRED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-return-value-ignored-inferred)

*   [RV: Return value of method without side effect is ignored (RV\_RETURN\_VALUE\_IGNORED\_NO\_SIDE\_EFFECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-return-value-ignored-no-side-effect)

*   [UC: Useless non-empty void method (UC\_USELESS\_VOID\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#uc-useless-void-method)


### IDivResultCastToDouble

This detector looks for places where the result of integer division is cast to double. Often, what was meant was to cast the integer operands to double and then perform the division.

*   [ICAST: Integral division result cast to double or float (ICAST\_IDIV\_CAST\_TO\_DOUBLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#icast-idiv-cast-to-double)

*   [ICAST: Integral value cast to double and then passed to Math.ceil (ICAST\_INT\_CAST\_TO\_DOUBLE\_PASSED\_TO\_CEIL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#icast-int-cast-to-double-passed-to-ceil)

*   [ICAST: int value cast to float and then passed to Math.round (ICAST\_INT\_CAST\_TO\_FLOAT\_PASSED\_TO\_ROUND)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#icast-int-cast-to-float-passed-to-round)


### FindBadCast2

This detector looks for bad casts of object references using data flow analysis.

*   [BC: Questionable cast to abstract collection (BC\_BAD\_CAST\_TO\_ABSTRACT\_COLLECTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-bad-cast-to-abstract-collection)

*   [BC: Questionable cast to concrete collection (BC\_BAD\_CAST\_TO\_CONCRETE\_COLLECTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-bad-cast-to-concrete-collection)

*   [BC: Impossible cast (BC\_IMPOSSIBLE\_CAST)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-impossible-cast)

*   [BC: Impossible downcast (BC\_IMPOSSIBLE\_DOWNCAST)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-impossible-downcast)

*   [BC: Impossible downcast of toArray() result (BC\_IMPOSSIBLE\_DOWNCAST\_OF\_TOARRAY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-impossible-downcast-of-toarray)

*   [BC: instanceof will always return false (BC\_IMPOSSIBLE\_INSTANCEOF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-impossible-instanceof)

*   [BC: Unchecked/unconfirmed cast (BC\_UNCONFIRMED\_CAST)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-unconfirmed-cast)

*   [BC: Unchecked/unconfirmed cast of return value from method (BC\_UNCONFIRMED\_CAST\_OF\_RETURN\_VALUE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-unconfirmed-cast-of-return-value)

*   [BC: instanceof will always return true (BC\_VACUOUS\_INSTANCEOF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bc-vacuous-instanceof)

*   [NP: A known null value is checked to see if it is an instance of a type (NP\_NULL\_INSTANCEOF)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-null-instanceof)


### FindUseOfNonSerializableValue

This detector looks for uses of non Serializable objects in contexts that require them to be serializable.

*   [DMI: Non serializable object written to ObjectOutput (DMI\_NONSERIALIZABLE\_OBJECT\_WRITTEN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-nonserializable-object-written)

*   [J2EE: Store of non serializable object into HttpSession (J2EE\_STORE\_OF\_NON\_SERIALIZABLE\_OBJECT\_INTO\_SESSION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#j2ee-store-of-non-serializable-object-into-session)


### BadSyntaxForRegularExpression

This detector looks for regular expressions that have invalid syntax.

*   [RE: Invalid syntax for regular expression (RE\_BAD\_SYNTAX\_FOR\_REGULAR\_EXPRESSION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#re-bad-syntax-for-regular-expression)

*   [RE: File.separator used for regular expression (RE\_CANT\_USE\_FILE\_SEPARATOR\_AS\_REGULAR\_EXPRESSION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#re-cant-use-file-separator-as-regular-expression)

*   [RE: “.” or “|” used for regular expression (RE\_POSSIBLE\_UNINTENDED\_PATTERN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#re-possible-unintended-pattern)


### VarArgsProblems

Looks for problems with arising from Java 5 varargs.

*   [VA: Primitive array passed to function expecting a variable number of object arguments (VA\_PRIMITIVE\_ARRAY\_PASSED\_TO\_OBJECT\_VARARG)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#va-primitive-array-passed-to-object-vararg)


### FindPuzzlers

This detector looks for miscellaneous small errors mentioned by Joshua Bloch and Neal Gafter in their work on Programming Puzzlers.

*   [BSHIFT: Possible bad parsing of shift operation (BSHIFT\_WRONG\_ADD\_PRIORITY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bshift-wrong-add-priority)

*   [Bx: Primitive value is boxed and then immediately unboxed (BX\_BOXING\_IMMEDIATELY\_UNBOXED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bx-boxing-immediately-unboxed)

*   [Bx: Primitive value is boxed then unboxed to perform primitive coercion (BX\_BOXING\_IMMEDIATELY\_UNBOXED\_TO\_PERFORM\_COERCION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bx-boxing-immediately-unboxed-to-perform-coercion)

*   [Bx: Primitive value is unboxed and coerced for ternary operator (BX\_UNBOXED\_AND\_COERCED\_FOR\_TERNARY\_OPERATOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bx-unboxed-and-coerced-for-ternary-operator)

*   [Bx: Boxed value is unboxed and then immediately reboxed (BX\_UNBOXING\_IMMEDIATELY\_REBOXED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#bx-unboxing-immediately-reboxed)

*   [DLS: Useless assignment in return statement (DLS\_DEAD\_LOCAL\_STORE\_IN\_RETURN)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dls-dead-local-store-in-return)

*   [DLS: Overwritten increment (DLS\_OVERWRITTEN\_INCREMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dls-overwritten-increment)

*   [DMI: Bad constant value for month (DMI\_BAD\_MONTH)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-bad-month)

*   [DMI: Adding elements of an entry set may fail due to reuse of Entry objects (DMI\_ENTRY\_SETS\_MAY\_REUSE\_ENTRY\_OBJECTS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-entry-sets-may-reuse-entry-objects)

*   [DMI: Invocation of hashCode on an array (DMI\_INVOKING\_HASHCODE\_ON\_ARRAY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-invoking-hashcode-on-array)

*   [USELESS\_STRING: Invocation of toString on an unnamed array (DMI\_INVOKING\_TOSTRING\_ON\_ANONYMOUS\_ARRAY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-invoking-tostring-on-anonymous-array)

*   [USELESS\_STRING: Invocation of toString on an array (DMI\_INVOKING\_TOSTRING\_ON\_ARRAY)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dmi-invoking-tostring-on-array)

*   [EC: Invocation of equals() on an array, which is equivalent to == (EC\_BAD\_ARRAY\_COMPARE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ec-bad-array-compare)

*   [BSHIFT: 32 bit int shifted by an amount not in the range -31..31 (ICAST\_BAD\_SHIFT\_AMOUNT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#icast-bad-shift-amount)

*   [ICAST: Result of integer multiplication cast to long (ICAST\_INTEGER\_MULTIPLY\_CAST\_TO\_LONG)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#icast-integer-multiply-cast-to-long)

*   [BSHIFT: Unsigned right shift cast to short/byte (ICAST\_QUESTIONABLE\_UNSIGNED\_RIGHT\_SHIFT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#icast-questionable-unsigned-right-shift)

*   [IC: Superclass uses subclass during initialization (IC\_SUPERCLASS\_USES\_SUBCLASS\_DURING\_INITIALIZATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ic-superclass-uses-subclass-during-initialization)

*   [IJU: JUnit assertion in run method will not be noticed by JUnit (IJU\_ASSERT\_METHOD\_INVOKED\_FROM\_RUN\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#iju-assert-method-invoked-from-run-method)

*   [IM: Computation of average could overflow (IM\_AVERAGE\_COMPUTATION\_COULD\_OVERFLOW)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#im-average-computation-could-overflow)

*   [IM: Check for oddness that won’t work for negative numbers (IM\_BAD\_CHECK\_FOR\_ODD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#im-bad-check-for-odd)

*   [IM: Integer multiply of result of integer remainder (IM\_MULTIPLYING\_RESULT\_OF\_IREM)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#im-multiplying-result-of-irem)

*   [PZ: Don’t reuse entry objects in iterators (PZ\_DONT\_REUSE\_ENTRY\_OBJECTS\_IN\_ITERATORS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#pz-dont-reuse-entry-objects-in-iterators)

*   [RV: Negating the result of compareTo()/compare() (RV\_NEGATING\_RESULT\_OF\_COMPARETO)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-negating-result-of-compareto)


### IntCast2LongAsInstant

Finds uses of 32-bit values to describe milliseconds since the epoch.

*   [ICAST: int value converted to long and used as absolute time (ICAST\_INT\_2\_LONG\_AS\_INSTANT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#icast-int-2-long-as-instant)


### FindSleepWithLockHeld

This detector looks for calls to Thread.sleep() made with a lock held. It is a slow detector.

*   [SWL: Method calls Thread.sleep() with a lock held (SWL\_SLEEP\_WITH\_LOCK\_HELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#swl-sleep-with-lock-held)


### DuplicateBranches

This detector looks for if/else or switch statements that have the same code for two branches, thus rendering the test useless. This often is caused by copying and pasting the two branches, causing incorrect logic for the one branch.

*   [DB: Method uses the same code for two branches (DB\_DUPLICATE\_BRANCHES)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#db-duplicate-branches)

*   [DB: Method uses the same code for two switch clauses (DB\_DUPLICATE\_SWITCH\_CLAUSES)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#db-duplicate-switch-clauses)


### XMLFactoryBypass

This detector looks for direct allocations of implementations of XML interfaces. This ties the code to a specific implementation, rather than using the supplied factory pattern to create these objects.

*   [XFB: Method directly allocates a specific implementation of xml interfaces (XFB\_XML\_FACTORY\_BYPASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#xfb-xml-factory-bypass)


### ConfusedInheritance

This detector looks for final classes that declare protected members. As this class cannot be derived from, the use of protected access for members is incorrect. The access should be changed to public or private to represent the correct intention of the field. This was probably caused by a change in use for this class, without completely changing all of the class to the new paradigm.

*   [CI: Class is final but declares protected field (CI\_CONFUSED\_INHERITANCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ci-confused-inheritance)


### QuestionableBooleanAssignment

This detector looks for simple assignments of literal boolean values to variables in conditional expressions.

*   [QBA: Method assigns boolean literal in boolean expression (QBA\_QUESTIONABLE\_BOOLEAN\_ASSIGNMENT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#qba-questionable-boolean-assignment)


### AppendingToAnObjectOutputStream

Looks for an attempt to append to an object output stream.

*   [IO: Doomed attempt to append to an object output stream (IO\_APPENDING\_TO\_OBJECT\_OUTPUT\_STREAM)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#io-appending-to-object-output-stream)


### StaticCalendarDetector

This detector warns about static fields of type java.util.Calendar or java.text.DateFormat (and subclasses) because Calendars are inherently unsafe for multithreaded use.

*   [STCAL: Call to static Calendar (STCAL\_INVOKE\_ON\_STATIC\_CALENDAR\_INSTANCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#stcal-invoke-on-static-calendar-instance)

*   [STCAL: Call to static DateFormat (STCAL\_INVOKE\_ON\_STATIC\_DATE\_FORMAT\_INSTANCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#stcal-invoke-on-static-date-format-instance)

*   [STCAL: Static Calendar field (STCAL\_STATIC\_CALENDAR\_INSTANCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#stcal-static-calendar-instance)

*   [STCAL: Static DateFormat (STCAL\_STATIC\_SIMPLE\_DATE\_FORMAT\_INSTANCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#stcal-static-simple-date-format-instance)


### CheckTypeQualifiers

Check for violations of properties specified by JSR-305 type qualifier annotations.

*   [TQ: Value annotated as carrying a type qualifier used where a value that must not carry that qualifier is required (TQ\_ALWAYS\_VALUE\_USED\_WHERE\_NEVER\_REQUIRED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tq-always-value-used-where-never-required)

*   [TQ: Comparing values with incompatible type qualifiers (TQ\_COMPARING\_VALUES\_WITH\_INCOMPATIBLE\_TYPE\_QUALIFIERS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tq-comparing-values-with-incompatible-type-qualifiers)

*   [TQ: Value required to have type qualifier, but marked as unknown (TQ\_EXPLICIT\_UNKNOWN\_SOURCE\_VALUE\_REACHES\_ALWAYS\_SINK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tq-explicit-unknown-source-value-reaches-always-sink)

*   [TQ: Value required to not have type qualifier, but marked as unknown (TQ\_EXPLICIT\_UNKNOWN\_SOURCE\_VALUE\_REACHES\_NEVER\_SINK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tq-explicit-unknown-source-value-reaches-never-sink)

*   [TQ: Value that might not carry a type qualifier is always used in a way requires that type qualifier (TQ\_MAYBE\_SOURCE\_VALUE\_REACHES\_ALWAYS\_SINK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tq-maybe-source-value-reaches-always-sink)

*   [TQ: Value that might carry a type qualifier is always used in a way prohibits it from having that type qualifier (TQ\_MAYBE\_SOURCE\_VALUE\_REACHES\_NEVER\_SINK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tq-maybe-source-value-reaches-never-sink)

*   [TQ: Value annotated as never carrying a type qualifier used where value carrying that qualifier is required (TQ\_NEVER\_VALUE\_USED\_WHERE\_ALWAYS\_REQUIRED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tq-never-value-used-where-always-required)

*   [TQ: Value without a type qualifier used where a value is required to have that qualifier (TQ\_UNKNOWN\_VALUE\_USED\_WHERE\_ALWAYS\_STRICTLY\_REQUIRED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#tq-unknown-value-used-where-always-strictly-required)


### CrossSiteScripting

This detector looks for obvious/blatant cases of cross site scripting vulnerabilities.

*   [HRS: HTTP cookie formed from untrusted input (HRS\_REQUEST\_PARAMETER\_TO\_COOKIE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#hrs-request-parameter-to-cookie)

*   [HRS: HTTP Response splitting vulnerability (HRS\_REQUEST\_PARAMETER\_TO\_HTTP\_HEADER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#hrs-request-parameter-to-http-header)

*   [PT: Absolute path traversal in servlet (PT\_ABSOLUTE\_PATH\_TRAVERSAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#pt-absolute-path-traversal)

*   [PT: Relative path traversal in servlet (PT\_RELATIVE\_PATH\_TRAVERSAL)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#pt-relative-path-traversal)

*   [XSS: JSP reflected cross site scripting vulnerability (XSS\_REQUEST\_PARAMETER\_TO\_JSP\_WRITER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#xss-request-parameter-to-jsp-writer)

*   [XSS: Servlet reflected cross site scripting vulnerability in error page (XSS\_REQUEST\_PARAMETER\_TO\_SEND\_ERROR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#xss-request-parameter-to-send-error)

*   [XSS: Servlet reflected cross site scripting vulnerability (XSS\_REQUEST\_PARAMETER\_TO\_SERVLET\_WRITER)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#xss-request-parameter-to-servlet-writer)


### DontIgnoreResultOfPutIfAbsent

Checks that if the result of putIfAbsent is ignored, the value passed as the second argument is not reused.

*   [RV: Return value of putIfAbsent ignored, value passed to putIfAbsent reused (RV\_RETURN\_VALUE\_OF\_PUTIFABSENT\_IGNORED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#rv-return-value-of-putifabsent-ignored)


### ReadOfInstanceFieldInMethodInvokedByConstructorInSuperclass

Checks for methods invoked from constructors for superclasses.

*   [UR: Uninitialized read of field method called from constructor of superclass (UR\_UNINIT\_READ\_CALLED\_FROM\_SUPER\_CONSTRUCTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ur-uninit-read-called-from-super-constructor)


### AtomicityProblem

Finds sequences of operations (e.g., get/put) on a concurrent abstraction that will not be executed atomically.

*   [AT: Sequence of calls to concurrent abstraction may not be atomic (AT\_OPERATION\_SEQUENCE\_ON\_CONCURRENT\_ABSTRACTION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#at-operation-sequence-on-concurrent-abstraction)


### DefaultEncodingDetector

Checks for calls to methods which perform a byte to String (or String to byte) conversion using the user's default platform encoding. This can cause the application behavior to vary between platforms.

*   [Dm: Reliance on default encoding (DM\_DEFAULT\_ENCODING)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#dm-default-encoding)


### CheckRelaxingNullnessAnnotation

Checks that overriding methods do not relax @Nonnull (made @CheckForNull) on return values or @CheckForNull (made @Nonnull) on parameters.

*   [NP: Method tightens nullness annotation on parameter (NP\_METHOD\_PARAMETER\_TIGHTENS\_ANNOTATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-method-parameter-tightens-annotation)

*   [NP: Method relaxes nullness annotation on return value (NP\_METHOD\_RETURN\_RELAXING\_ANNOTATION)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#np-method-return-relaxing-annotation)


### DontAssertInstanceofInTests

Detector for patterns in JUnit tests where the type of an object is checked by asserting the instanceof operator.

This should be avoided as the ClassCastException that would result from an improper cast may provide more information regarding the cause of the error than a "false is not true" message which would result from asserting the result of the instanceof operator.

It is a fast detector

*   [JUA: Asserting value of instanceof in tests is not recommended. (JUA\_DONT\_ASSERT\_INSTANCEOF\_IN\_TESTS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#jua-dont-assert-instanceof-in-tests)


### FindBadEndOfStreamCheck

Detector for patterns where the return value of java.io.FileInputStream.read() or java.io.FileReader.read() is converted before checking against -1.

Both methods return an int. If this int is converted to byte (in the case of FileInputStream.read()) then -1 and the byte 0xFF become indistinguishable. If it is converted to char (in the case of FileReader.read()) then -1 becomes 0xFFFF which is Character.MAX\_VALUE since characters are unsigned in Java.

*   [EOS: Data read is converted before comparison to -1 (EOS\_BAD\_END\_OF\_STREAM\_CHECK)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#eos-bad-end-of-stream-check)


### ReflectionIncreaseAccessibility

Detector for public methods instantiating a class they get in their parameter.

An attacker may invoke this method with a class that has no public constructor.

*   [REFLC: Public method uses reflection to create a class it gets in its parameter which could increase the accessibility of any class (REFLC\_REFLECTION\_MAY\_INCREASE\_ACCESSIBILITY\_OF\_CLASS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#reflc-reflection-may-increase-accessibility-of-class)

*   [REFLF: Public method uses reflection to modify a field it gets in its parameter which could increase the accessibility of any class (REFLF\_REFLECTION\_MAY\_INCREASE\_ACCESSIBILITY\_OF\_FIELD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#reflf-reflection-may-increase-accessibility-of-field)


### FindOverridableMethodCall

Detector for patterns where a constructor, a clone(), or a readObject() method calls an overridable method.

Calling an overridable method from a constructor may result in the use of uninitialized data. Calling such method from a clone(), or readObject() method is insecure.

*   [MC: An overridable method is called from the clone() method. (MC\_OVERRIDABLE\_METHOD\_CALL\_IN\_CLONE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mc-overridable-method-call-in-clone)

*   [MC: An overridable method is called from a constructor (MC\_OVERRIDABLE\_METHOD\_CALL\_IN\_CONSTRUCTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mc-overridable-method-call-in-constructor)

*   [MC: An overridable method is called from the readObject method. (MC\_OVERRIDABLE\_METHOD\_CALL\_IN\_READ\_OBJECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#mc-overridable-method-call-in-read-object)


### ConstructorThrow

Finds constructors that throw exceptions.

*   [CT: Be wary of letting constructors throw exceptions. (CT\_CONSTRUCTOR\_THROW)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ct-constructor-throw)


### FindInstanceLockOnSharedStaticData

Detector for patterns where a shared static data is modified by either an instance level non-static synchronized method, or inside a synchronized block, which used a non-static lock object.

Programs must not use instance locks to protect static shared data because instance locks are ineffective when two or more instances of the class are created. Consequently, failure to use a static lock object leaves the shared state unprotected against concurrent access.

*   [SSD: Instance level lock was used on a shared static data (SSD\_DO\_NOT\_USE\_INSTANCE\_LOCK\_ON\_SHARED\_STATIC\_DATA)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ssd-do-not-use-instance-lock-on-shared-static-data)


### DontUseFloatsAsLoopCounters

Checks for floats in loop counters.

*   [FL: Do not use floating-point variables as loop counters (FL\_FLOATS\_AS\_LOOP\_COUNTERS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#fl-floats-as-loop-counters)


### PermissionsSuper

Checks method getPermissions() of classes implementing interface java.security.SecureClassLoader. The methods must always call super.getPermissions() to get the initial value of the object which they return at the end.

*   [PERM: Custom class loader does not call its superclass’s getPermissions() (PERM\_SUPER\_NOT\_CALLED\_IN\_GETPERMISSIONS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#perm-super-not-called-in-getpermissions)


### FindPotentialSecurityCheckBasedOnUntrustedSource

Looks for potential security checks on an untrusted source before entering a doPrivileged block.

*   [USC: Potential security check based on untrusted source. (USC\_POTENTIAL\_SECURITY\_CHECK\_BASED\_ON\_UNTRUSTED\_SOURCE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#usc-potential-security-check-based-on-untrusted-source)


### FindAssertionsWithSideEffects

Finds assertions with side effects.

*   [ASE: Expression in assertion may produce a side effect (ASE\_ASSERTION\_WITH\_SIDE\_EFFECT)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ase-assertion-with-side-effect)

*   [ASE: Method invoked in assertion may produce a side effect (ASE\_ASSERTION\_WITH\_SIDE\_EFFECT\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#ase-assertion-with-side-effect-method)


### FindPublicAttributes

This detector looks for public attributes that are also written by the methods of the class.

*   [PA: Array-type field is public (PA\_PUBLIC\_ARRAY\_ATTRIBUTE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#pa-public-array-attribute)

*   [PA: Mutable object-type field is public (PA\_PUBLIC\_MUTABLE\_OBJECT\_ATTRIBUTE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#pa-public-mutable-object-attribute)

*   [PA: Primitive field is public (PA\_PUBLIC\_PRIMITIVE\_ATTRIBUTE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#pa-public-primitive-attribute)


### FindVulnerableSecurityCheckMethods

Methods that perform security checks should be prevented from being overridden, so they must be declared as private or final. Otherwise, these methods can be compromised when a malicious subclass overrides them and omits the checks.

*   [VSC: Non-Private and non-final security check methods are vulnerable (VSC\_VULNERABLE\_SECURITY\_CHECK\_METHODS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#vsc-vulnerable-security-check-methods)


### FindArgumentAssertions

Finds assertions that validate public method arguments.

*   [AA: Assertion is used to validate an argument of a public method (AA\_ASSERTION\_OF\_ARGUMENTS)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#aa-assertion-of-arguments)


### UnnecessaryEnvUsage

Checks for calls of System.getenv(), where the variable has an equivalent Java property too.

*   [ENV: It is preferable to use portable Java property instead of environment variable. (ENV\_USE\_PROPERTY\_INSTEAD\_OF\_ENV)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#env-use-property-instead-of-env)


### MultipleInstantiationsOfSingletons

This detector looks for violations of the idioms for writing classes using singleton design pattern.

*   [SING: Instance-getter method of class using singleton design pattern is not synchronized. (SING\_SINGLETON\_GETTER\_NOT\_SYNCHRONIZED)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sing-singleton-getter-not-synchronized)

*   [SING: Class using singleton design pattern has non-private constructor. (SING\_SINGLETON\_HAS\_NONPRIVATE\_CONSTRUCTOR)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sing-singleton-has-nonprivate-constructor)

*   [SING: Class using singleton design pattern directly implements Cloneable interface. (SING\_SINGLETON\_IMPLEMENTS\_CLONEABLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sing-singleton-implements-cloneable)

*   [SING: Class using singleton design pattern implements clone() method without being an unconditional CloneNotSupportedException-thrower. (SING\_SINGLETON\_IMPLEMENTS\_CLONE\_METHOD)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sing-singleton-implements-clone-method)

*   [SING: Class using singleton design pattern directly or indirectly implements Serializable interface. (SING\_SINGLETON\_IMPLEMENTS\_SERIALIZABLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sing-singleton-implements-serializable)

*   [SING: Class using singleton design pattern indirectly implements Cloneable interface. (SING\_SINGLETON\_INDIRECTLY\_IMPLEMENTS\_CLONEABLE)](https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html#sing-singleton-indirectly-implements-cloneable)
