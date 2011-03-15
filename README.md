Based on the functionality of the Perl implementation of sprintf.

## sprintf syntax

The format is specified using the `%{flags}{type}` convention, for example `%s` to
insert a string at the position. Following types is possible (faithfully
stolen from perldoc):

  * `%%` a percent sign

  * `%c` a character with the given number

  * `%s` a string

  * `%d` a signed integer, in decimal

  * `%u` an unsigned integer, in decimal

  * `%o` an unsigned integer, in octal

  * `%x` an unsigned integer, in hexadecimal

  * `%e` a floating-point number, in scientific notation

  * `%f` a floating-point number, in fixed decimal notation

  * `%g` a floating-point number, in `%e` or `%f` notation

  * `%X` like `%x`, but using upper-case letters

  * `%E` like `%e`, but using an upper-case `E`

  * `%G` like `%g`, but with an upper-case `E` (if applicable)

  * `%b` an unsigned integer, in binary

  * `%B` like `%b`, but using an upper-case `B` with the # flag

Following flags exists:

  * `space` prefix positive number with a space

  * `+` prefix positive number with a plus sign

  * `-` left-justify within the field

  * `0` use zeros, not spaces, to right-justify

  * `#` ensure the leading `0` for any octal, prefix non-zero hexadecimal with
`0x` or `0X`, prefix non-zero binary with `0b` or `0B`

  * `@` - if applying vectorization to an Number, then `@N` will define the
bitwidth

see perldoc -f sprintf for more information about how to use the flags. This
module handles mosly everything the perl module handles, except the `%n` and `%p`
types and size modifiers for integers.

## Global functions

Following global functions is exported

### `$.printf( format: string, arg1, arg2, ...);`

Will print out the string to the console, or using window.dump()

### `$.vprintf( format: string, [arg1, arg2, ...]);`

Will print out the string to the console, or using window.dump()

### `$.sprintf( format: string, arg1, arg2, ...);`

Will return a formated string

### `$.vsprintf( format: string, [arg1, arg2, ...]);`

Will return a formated string

## Member functions

### `$().printf( format: string, arg1, arg2, ...);`

Will append the formated string.

### `$().vprintf( format: string, [arg1, arg2, ...]);`

Will append the formated string.

### `$().format( arg1, arg2, ...);`

Will format the objects in question with given arguments

### `$().vformat( [ arg1, arg2, ... ] );`

Will format the objects in question with given arguments

## Examples

### Different types of types

    $('obj').printf('<div>Integer: %d, hex: %1$#x, HEX: %1$#X, Binary: %1$#b,
	BINARY: %1$#B, Octal: %1$#o, Float: %1$f, Exp: %1$e</div>', 123.456 );

results in

    Integer: 123, hex: 0x7b, HEX: 0x7B, Binary: 0b1111011, BINARY: 0B1111011,
	Octal: 0173, Float: 123.456, Exp: 1.234560e+2

appended to the objects in question.

### Vector parameter

    $('obj').printf("%0*v8b", ' ', "12345" );

results in

    00110001 00110010 00110011 00110100 00110101

appended to the objects in question.


    $('#target').printf('<div>The color <strong>#%*2$vX</strong> can also be
	written as an RGB triplet:  <strong>rgb(%*3$v1$d)</strong></div>',
	String.fromCharCode(0x33,0xab,0x67), '', ', '  );

	$('#target').printf('<div>The color <strong>#%*2$vX</strong> can also be
	written as an RGB triplet:  <strong>rgb(%*3$v1$d)</strong></div>',
	[0x33,0xab,0x67], '', ', '  );

	$('#target').printf('<div>The color <strong>#%@8*2$vX</strong> can also be
	written as an RGB triplet:  <strong>rgb(%@8*3$v1$d)</strong></div>', 0x33ab67,
	'', ', '  );

	$('#target').printf('<div>The color <strong>#%@8*2$vX</strong> can also be
	written as an RGB triplet:  <strong>rgb(%@8*3$v1$d)</strong></div>', 3386215,
	'', ', '  );


will all results in

    The color <strong>#33AB67</strong> can also be written as an RGB triplet:
	<strong>rgb(51, 171, 103)</strong>

(perhaps not the most useful code, but it shows some sort of possibility :))

### format

    $('.target').format( 'Hello', 'World'  );

with the html

    <div class="target">
        <div>
			<strong>%s</strong> <em>%s</em>
        </div>
    </div>

will result in

    <div class="target">
        <div>
			<strong>Hello</strong> <em>World</em>
        </div>
    </div>
