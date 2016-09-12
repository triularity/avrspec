Basic specifications for various AVR microprocessors.

Format (subject to significant change):

Any text after a hash (#) is treated as a comment and ignored.

Certain types may have conditions (preceded by a question mark (?)). These
control when the entry applies.

	Exclude for specific core(s):
		!<core>[/<core>[/<core>...]]

	Only applies for specific core(s):
		<core>[/<core>[/<core>...]]


VERSION <version>

	Define the version of the specification file.

	version		The version in YYYY.MM.DD([a-z]) format (GMT time).


CORE <mcu> <pre-processor>

	Define a core that applies to this specification.

	mcu		The avr-gcc value for -mmcu=.
			This is also used as the core ID.

	pre-processor	The built-in macro defined during compile for the
			target. This is typically in the form __AVR_ATxxxxxx__.


FUNC <id> [<alternates>] [?<conditions>]

	Declare pin function(s).

	id		The primary function ID.

	alternates	Alternative function IDs that apply. Multiple values
			are separated by a slash (/).

	conditions	Conditions that control when the function applies.

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


OPTION <name> [<value>] [?<conditions>]

	Define an option.

	name		A symbol name.

	value		The value the option is set to.

	conditions	Conditions that control when the function applies.

	Defined options:

		ADCSRB_ADLAR	The ADCSRB register contains the ADLAR bit.
		ADCSRB_MUX5	The ADCSRB register contains the MUX5 bit.
		ADCSRB_REFS2	The ADCSRB register contains the REFS2 bit.
		ADMUXB_MUX5	The ADMUXB register contains the MUX5 bit.
		ADMUX_ADLAR	The ADMUX register contains the ADLAR bit.
		ADMUX_MUX5	The ADMUX register contains the MUX5 bit.
		ADMUX_REFS2	The ADMUX register contains the REFS2 bit.
		MCUCR_PUD	The MCUCR register contains the PUD bit.
		SFIOR_PUD	The SFIOR register contains the PUD bit.
		HIGH_IOM	The core has I/O addressed > 0xFF.
		MUX		The value is the highest MUXn bit
				(e.g. 3 = MUX3)
				If not set, there is no MUX value.
		REFS		The value is the highest REFSn bit
				(e.g. 2 = REFS2)
				If not set, there is no REFS value.
		OCnx_TCCR	Override the normal TCCRnx register used for
				OCnx with the one this specifies (e.g. GTCCR).
		OCnx_TCCR_EXTRA	Extra named bits to set in the TCCR when the
				OCnx is enabled (e.g. PWM1A).
		OCnx_REMAP	The timer is only connected to the function
				specified when in remap mode.
		PROGMEM_SIZE	The value is the flash/PROGMEM size in bytes.
		RAM_SIZE	The value is the internal SRAM size in bytes.
		EEPROM_SIZE	The value is the EEPROM size in bytes.
				If not set, there is no EEPROM.


MAP <field> <id> <value>

	Map a field value.

	field		The field to map.

	id		The value name/identifier.

	value		The mapped number value.


ADC_MUX <func-id> <channel>

	func-id		A source function.

	channel		The channel number that maps to an ADC MUX value.


PAD <func-id> <sockets> <number>

	Define a PAD pin.

	func-id		The function ID. This must match the ID declared
			in an FUNC entry (if declared). Unused/Not-Connected
			pins should use a minus (-).

	sockets		The socket format(s) that this applies to.

	number		The physical pin number/identifier.

