Basic specifications for various AVR microprocessors.

Format (subject to significant change):

Any text after a hash (#) is treated as a comment and ignored.


CORE <mcu> <pre-processor>

	Define a core that applies to this specification.

	mcu		The avr-gcc value for -mmcu=.
			This is also used as the core ID.

	pre-processor	The built-in macro defined during compile for the
			target. This is typically in the form __AVR_ATxxxxxx__.


FUNC <id> [<alternates>] [<conditions>]

	Declare pin function(s).

	id		The primary function ID.

	alternates	Alternative function IDs that apply. Multiple values
			are separated by a slash (/).

	conditions	Conditions that control when the function applies.

			Exclude for specific cores:
				!<core>[/<core>[/<core>...]]

	IDs must start with a letter, followed by zero or more letters (A-Z),
	numbers (0-9), or underscores (_). IDs are normally only uppercase,
	expect for special cases (e.g. "dW").

	IDs that are inverted are prefixed with a minus (-).

	Additional function details may follow the ID, indicated by a
	tilde (~) and a function specific value.

		OCnx~<timer-bits>


GPIO <func-id> <names> [<index>]

	Define a logical GPIO pin.

	func-id		The function ID. This must be declared by a FUNC or
			or ADC_MUX entry.

	names		The digital and/or analog tag names in the form of
			Dn and An. Multiple valuesare separated by a slash (/).

	index		The GPIO pin index. By default this is taken from the
			digital pin name (e.g. D3). If both are specified,
			then they must match. Entries without specified index
			will be added after all defined indexes.


OPTION <name> [<value>]

	Define an option.

	name		A symbol name.

	value		The value the option is set to.


ADC_REF <func-id> <value>

	func-id		A source function.

	value		The index that maps to a REFS value.


ADC_MUX <func-ids> <channel>

	func-ids	A source function. Multiple values are separated by
			a slash (/).

	channel		The channel number that maps to a MUX value.


PAD <func-id> <sockets> <number>

	Define a PAD pin.

	func-id		The function ID. This must match the ID declared
			in an FUNC entry (if declared). Unused/Not-Connected
			pins should use a minus (-).

	sockets		The socket format(s) that this applies to.

	number		The physical pin number/identifier.

