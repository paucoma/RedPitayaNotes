==============
SCPI Commands
==============

.. code-block:: c

    scpi_t scpi_context = {
        .cmdlist = scpi_commands,
        .buffer = {
            .length = SCPI_INPUT_BUFFER_LENGTH,
            .data = scpi_input_buffer,
        },
        .interface = &scpi_interface,
        .registers = scpi_regs,
        .units = scpi_units_def,
        .idn = {"REDPITAYA", "INSTR2014", NULL, "01-02"},
    };
..

Extracted from `RedPitaya/scpi-server/src/scpi-commands.c - 3e2e3fd on 29 Oct 2015 <https://github.com/RedPitaya/RedPitaya/blob/f548c0ed3b93c061fc115eac27013db62f927f6c/scpi-server/src/scpi-commands.c>`_ and formatted on 2016/09/02

:code:`static const scpi_command_t scpi_commands[] = {`

IEEE Mandated Commands (SCPI std V1999.0 4.1.1)
================================================

+-----------+---------------+
| Command   | Function()    |
+===========+===============+   
| "*CLS"    | SCPI_CoreCls  |
+-----------+---------------+
| "*ESE"    | SCPI_CoreEse  |
+-----------+---------------+
| "*ESE?"   | SCPI_CoreEseQ |
+-----------+---------------+
| "*ESR?"   | SCPI_CoreEsrQ |
+-----------+---------------+
| "*IDN?"   | SCPI_CoreIdnQ |
+-----------+---------------+
| "*OPC"    | SCPI_CoreOpc  |
+-----------+---------------+
| "*OPC?"   | SCPI_CoreOpcQ |
+-----------+---------------+
| "*RST"    | SCPI_CoreRst  |
+-----------+---------------+
| "*SRE"    | SCPI_CoreSre  |
+-----------+---------------+
| "*SRE?"   | SCPI_CoreSreQ |
+-----------+---------------+
| "*STB?"   | SCPI_CoreStbQ |
+-----------+---------------+
| "*TST?"   | SCPI_CoreTstQ |
+-----------+---------------+
| "*WAI"    | SCPI_CoreWai  |
+-----------+---------------+

Required SCPI commands (SCPI std V1999.0 4.2.1) 
================================================

+----------------------------------------+---------------------------------+
| Command                                | Function()                      |
+========================================+=================================+   
| "SYSTem:ERRor[:NEXT]?"                 |  SCPI_SystemErrorNextQ          |
+----------------------------------------+---------------------------------+
| "SYSTem:ERRor:COUNt?"                  |  SCPI_SystemErrorCountQ         |
+----------------------------------------+---------------------------------+
| "SYSTem:VERSion?"                      |  SCPI_SystemVersionQ            |
+----------------------------------------+---------------------------------+
| "STATus:QUEStionable[:EVENt]?"         |  SCPI_StatusQuestionableEventQ  |
+----------------------------------------+---------------------------------+
| "STATus:QUEStionable:ENABle"           |  SCPI_StatusQuestionableEnable  |
+----------------------------------------+---------------------------------+
| "STATus:QUEStionable:ENABle?"          |  SCPI_StatusQuestionableEnableQ |
+----------------------------------------+---------------------------------+
| "STATus:PRESet"                        |  SCPI_StatusPreset              |
+----------------------------------------+---------------------------------+
| "SYSTem:COMMunication:TCPIP:CONTROL?"  |  SCPI_SystemCommTcpipControlQ   |
+----------------------------------------+---------------------------------+
| "ECHO?"                                |  SCPI_Echo                      |
+----------------------------------------+---------------------------------+
| "ECO:VERSION?"                         |  SCPI_EchoVersion               |
+----------------------------------------+---------------------------------+


RedPitaya
==========

-----------------
General commands
-----------------

+------------------+---------------+-------------------------+
| Command          | Arguments     |  Function()             |
+==================+===============+=========================+   
| "RP:INit"        |               | RP_InitAll              |
+------------------+---------------+-------------------------+
| "RP:REset"       |               | RP_ResetAll             |
+------------------+---------------+-------------------------+
| "RP:RELease"     |               | RP_ReleaseAll           |
+------------------+---------------+-------------------------+
| "RP:FPGABITREAM" |               | RP_FpgaBitStream        |
+------------------+---------------+-------------------------+
| "RP:DIg[:loop]"  |               | RP_EnableDigLoop        |
+------------------+---------------+-------------------------+


+------------------+---------------+-------------------------+
| Command          | Arguments     |  Function()             |
+==================+===============+=========================+   
| "DIG:RST"        |               | RP_DigitalPinReset      |
+------------------+---------------+-------------------------+
| "DIG:PIN"        | <pin>,<state> | RP_DigitalPinState      |
+------------------+---------------+-------------------------+
| "DIG:PIN?"       |  <pin>        | RP_DigitalPinStateQ     |
+------------------+---------------+-------------------------+
| "DIG:PIN:DIR"    | <dir>,<pin>   | RP_DigitalPinDirection  |
+------------------+---------------+-------------------------+
| "DIG:PIN:DIR?"   |  <pin>        | RP_DigitalPinDirectionQ |
+------------------+---------------+-------------------------+

  * :code:`<pin>` = 
  
    * :code:`DIO`[1..7]:code:`_`[P,N] 
    * :code:`DIO0_N`
    * :code:`LED`[1..8]
  * :code:`<dir>` = {:code:`OUTP`,:code:`INP`} 

    * default : :code:`OUTP`
  * :code:`<state>` = {0,1}

    * default : :code:`0`

+------------------+---------------+-------------------------+
| Command          | Arguments     |  Function()             |
+==================+===============+=========================+   
| "ANALOG:RST"     |               | RP_AnalogPinReset       |
+------------------+---------------+-------------------------+
| "ANALOG:PIN"     | <pin>,<value> | RP_AnalogPinValue       |
+------------------+---------------+-------------------------+
| "ANALOG:PIN?"    |  <pin>        | RP_AnalogPinValueQ      |
+------------------+---------------+-------------------------+

  * :code:`<pin>` = 

    * :code:`AOUT`[0..3]
    * :code:`AIN`[0..3]

      * return volts : [:code:`0` - :code:`3.3`] V
  * :code:`<value>` = 

    * outputs : [:code:`0` - :code:`1.8`] V
    * default : :code:`0`

--------
Acquire
--------

+----------------------------+----------------------------+
| Command                    | Function()                 |
+============================+============================+ 
| "ACQ:START"                |  RP_AcqStart               |
+----------------------------+----------------------------+
| "ACQ:STOP"                 |  RP_AcqStop                |
+----------------------------+----------------------------+
| "ACQ:RST"                  |  RP_AcqReset               |
+----------------------------+----------------------------+
| "ACQ:DEC"                  |  RP_AcqDecimation          |
+----------------------------+----------------------------+
| "ACQ:DEC?"                 |  RP_AcqDecimationQ         |
+----------------------------+----------------------------+
| "ACQ:SRAT?"                |  RP_AcqSamplingRateHzQ     |
+----------------------------+----------------------------+
| "ACQ:AVG"                  |  RP_AcqAveraging           |
+----------------------------+----------------------------+
| "ACQ:AVG?"                 |  RP_AcqAveragingQ          |
+----------------------------+----------------------------+
| "ACQ:TRIG"                 |  RP_AcqTriggerSrc          |
+----------------------------+----------------------------+
| "ACQ:TRIG:STAT?"           |  RP_AcqTriggerSrcQ         |
+----------------------------+----------------------------+
| "ACQ:TRIG:DLY"             |  RP_AcqTriggerDelay        |
+----------------------------+----------------------------+
| "ACQ:TRIG:DLY?"            |  RP_AcqTriggerDelayQ       |
+----------------------------+----------------------------+
| "ACQ:TRIG:DLY:NS"          |  RP_AcqTriggerDelayNs      |
+----------------------------+----------------------------+
| "ACQ:TRIG:DLY:NS?"         |  RP_AcqTriggerDelayNsQ     |
+----------------------------+----------------------------+
| "ACQ:TRIG:HYST"            |  RP_AcqTriggerHyst         |
+----------------------------+----------------------------+
| "ACQ:TRIG:HYST?"           |  RP_AcqTriggerHystQ        |
+----------------------------+----------------------------+
| "ACQ:SOUR#:GAIN"           |  RP_AcqGain                |
+----------------------------+----------------------------+
| "ACQ:SOUR#:GAIN?"          |  RP_AcqGainQ               |
+----------------------------+----------------------------+
| "ACQ:TRIG:LEV"             |  RP_AcqTriggerLevel        |
+----------------------------+----------------------------+
| "ACQ:TRIG:LEV?"            |  RP_AcqTriggerLevelQ       |
+----------------------------+----------------------------+
| "ACQ:WPOS?"                |  RP_AcqWritePointerQ       |
+----------------------------+----------------------------+
| "ACQ:TPOS?"                |  RP_AcqWritePointerAtTrigQ |
+----------------------------+----------------------------+
| "ACQ:DATA:UNITS"           |  RP_AcqScpiDataUnits       |
+----------------------------+----------------------------+
| "ACQ:DATA:UNITS?"          |  RP_AcqScpiDataUnitsQ      |
+----------------------------+----------------------------+
| "ACQ:DATA:FORMAT"          |  RP_AcqSetDataFormat       |
+----------------------------+----------------------------+
| "ACQ:SOUR#:DATA:STA:END?"  |  RP_AcqDataPosQ            |
+----------------------------+----------------------------+
| "ACQ:SOUR#:DATA:STA:N?"    |  RP_AcqDataQ               |
+----------------------------+----------------------------+
| "ACQ:SOUR#:DATA:OLD:N?"    |  RP_AcqOldestDataQ         |
+----------------------------+----------------------------+
| "ACQ:SOUR#:DATA?"          |  RP_AcqDataOldestAllQ      |
+----------------------------+----------------------------+
| "ACQ:SOUR#:DATA:LAT:N?"    |  RP_AcqLatestDataQ         |
+----------------------------+----------------------------+
| "ACQ:BUF:SIZE?"            |  RP_AcqBufferSizeQ         |
+----------------------------+----------------------------+

---------
Generate
---------

+--------------------------+----------------------------+
| Command                  | Function()                 |
+==========================+============================+ 
| "GEN:RST"                |   RP_GenReset              |
+--------------------------+----------------------------+
| "OUTPUT#:STATE"          |   RP_GenState              |
+--------------------------+----------------------------+
| "OUTPUT#:STATE?"         |   RP_GenStateQ             |
+--------------------------+----------------------------+
| "SOUR#:FREQ:FIX"         |   RP_GenFrequency          |
+--------------------------+----------------------------+
| "SOUR#:FREQ:FIX?"        |   RP_GenFrequencyQ         |
+--------------------------+----------------------------+
| "SOUR#:FUNC"             |   RP_GenWaveForm           | 
+--------------------------+----------------------------+
| "SOUR#:FUNC?"            |   RP_GenWaveFormQ          |
+--------------------------+----------------------------+
| "SOUR#:VOLT"             |   RP_GenAmplitude          |
+--------------------------+----------------------------+
| "SOUR#:VOLT?"            |   RP_GenAmplitudeQ         |
+--------------------------+----------------------------+
| "SOUR#:VOLT:OFFS"        |   RP_GenOffset             |
+--------------------------+----------------------------+
| "SOUR#:VOLT:OFFS?"       |   RP_GenOffsetQ            |
+--------------------------+----------------------------+
| "SOUR#:PHAS"             |   RP_GenPhase              |
+--------------------------+----------------------------+
| "SOUR#:PHAS?"            |   RP_GenPhaseQ             |
+--------------------------+----------------------------+
| "SOUR#:DCYC"             |   RP_GenDutyCycle          |
+--------------------------+----------------------------+
| "SOUR#:DCYC?"            |   RP_GenDutyCycleQ         |
+--------------------------+----------------------------+
| "SOUR#:TRAC:DATA:DATA"   |   RP_GenArbitraryWaveForm  |
+--------------------------+----------------------------+
| "SOUR#:TRAC:DATA:DATA?"  |   RP_GenArbitraryWaveFormQ |
+--------------------------+----------------------------+
| "SOUR#:BURS:STAT"        |   RP_GenGenerateMode       | 
+--------------------------+----------------------------+
| "SOUR#:BURS:STAT?"       |   RP_GenGenerateModeQ      |
+--------------------------+----------------------------+
| "SOUR#:BURS:NCYC"        |   RP_GenBurstCount         |
+--------------------------+----------------------------+
| "SOUR#:BURS:NCYC?"       |   RP_GenBurstCountQ        |
+--------------------------+----------------------------+
| "SOUR#:BURS:NOR"         |   RP_GenBurstRepetitions   |
+--------------------------+----------------------------+
| "SOUR#:BURS:NOR?"        |   RP_GenBurstRepetitionsQ  |
+--------------------------+----------------------------+
| "SOUR#:BURS:INT:PER"     |   RP_GenBurstPeriod        |
+--------------------------+----------------------------+
| "SOUR#:BURS:INT:PER?"    |   RP_GenBurstPeriodQ       |
+--------------------------+----------------------------+
| "SOUR#:TRIG:SOUR"        |   RP_GenTriggerSource      |
+--------------------------+----------------------------+
| "SOUR#:TRIG:SOUR?"       |   RP_GenTriggerSourceQ     |
+--------------------------+----------------------------+
| "SOUR#:TRIG:IMM"         |   RP_GenTrigger            |
+--------------------------+----------------------------+

:code:`    SCPI_CMD_LIST_END  };`

Details
========

  * "SOUR#:FUNC"  -->  RP_GenWaveForm 

    * 0"SINE","SQUARE","TRIANGLE","SAWU","SAWD","PWM","DC","ARBITRARY"
  * "SOUR#:BURS:STAT"        RP_GenGenerateMode        

    * 0"CONTINUOUS","BURST","STREAM"
  * "SOUR#:TRIG:SOUR"        RP_GenTriggerSource       

    * 1"INT","EXT_PE","EXT_NE","GATED"