# CBT669
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 669 is from Willy Jensen.  Programs covered concerning    *   FILE 669
//*           REXX Global Variables, VSAM bulk access, OpComm etc   *   FILE 669
//*                                                                 *   FILE 669
//*       Contact email: willy@harders-jensen.com                   *   FILE 669
//*       Web:           http://harders-jensen.com                  *   FILE 669
//*                                                                 *   FILE 669
//*       Package date: 2024-dec-10                                 *   FILE 669
//*                                                                 *   FILE 669
//*       * See install notes at the end *                          *   FILE 669
//*                                                                 *   FILE 669
//*       Changes in this package:                                  *   FILE 669
//*        REXXGBLV - Fix abend S0c4 when IBMs Zero Address         *   FILE 669
//*                   testing is enabled.                           *   FILE 669
//*                 - Minor fixes.                                  *   FILE 669
//*        REXXVSAM - External SORT can now handle DFSPARMS         *   FILE 669
//*                   dataset, as well as DFSPARMS data in a        *   FILE 669
//*                   stem.                                         *   FILE 669
//*                   Some syntax enhancements.                     *   FILE 669
//*                                                                 *   FILE 669
//*        See the xxxxHIST members for history of products.        *   FILE 669
//*                                                                 *   FILE 669
//*       Programs in package:                                      *   FILE 669
//*                                                                 *   FILE 669
//*        ISPDPX01 - ISPF panel exit, supply panel lines in        *   FILE 669
//*                   REXX stem(s)                                  *   FILE 669
//*                   Build: 004 2022-09-04                         *   FILE 669
//*        ISPPDA   - ISPF panel with dynamic area, it handles      *   FILE 669
//*                   scrolling and line commands internally.       *   FILE 669
//*                   Build: 2024-02-13                             *   FILE 669
//*        REXXGBLV - REXX function to implement global             *   FILE 669
//*                   variables.                                    *   FILE 669
//*                   Build: 078.4 2024-12-18                       *   FILE 669
//*        REXXSTOR - REXX function to save and retrieve a          *   FILE 669
//*                   string in command storage.                    *   FILE 669
//*                   Build: 005 2019-12-04                         *   FILE 669
//*        REXXVARS - REXX general utility to browse, copy,         *   FILE 669
//*                   delete, edit, index, list, rename, sort       *   FILE 669
//*                   and view variables.                           *   FILE 669
//*                   Build: 012.6 2024-12-07                       *   FILE 669
//*        RXHLLK   - Assembler submodule to give hi-level          *   FILE 669
//*                   programs access to REXX services like         *   FILE 669
//*                   the variables, the TSO stack and more.        *   FILE 669
//*                   Build: 003 2024-04-30                         *   FILE 669
//*        RXOPCOMM - REXX function allowing a REXX program         *   FILE 669
//*                   to support operator MODIFY and STOP           *   FILE 669
//*                   commands.                                     *   FILE 669
//*                   Build: 008 2021-05-25                         *   FILE 669
//*        RXPATTRN - REXX function to test a string against        *   FILE 669
//*                   a pattern.                                    *   FILE 669
//*                   Build: 009.6 2023-07-03                       *   FILE 669
//*        RXPIPE   - Free REXX based alternative to the IBM        *   FILE 669
//*                   PIPE command (part of Batch Pipes).           *   FILE 669
//*                   Build: 007.11 2024-02-20.1                    *   FILE 669
//*        RXRDPRML - REXX function to copy a parmlib               *   FILE 669
//*                   member to a stem.                             *   FILE 669
//*                   Build: 005 2019-12-04                         *   FILE 669
//*        RXREALDS - REXX function returns real name for           *   FILE 669
//*                   relative gds or alias.                        *   FILE 669
//*                   Build: 002 2023-06-14 07:44:05                *   FILE 669
//*        RXVSAMBA - REXX function to read and update a            *   FILE 669
//*                   VSAM KSDS and RRDS database through           *   FILE 669
//*                   stem or stack.                                *   FILE 669
//*                   Build: 030 2024-08-09                         *   FILE 669
//*        RXWAIT   - REXX function to wait whole or                *   FILE 669
//*                   fractions of seconds.                         *   FILE 669
//*                   May also be used as a TSO command and         *   FILE 669
//*                   a batch pgm                                   *   FILE 669
//*                   Build: 002 2019-12-04                         *   FILE 669
//*                                                                 *   FILE 669
//*       Install a program                                         *   FILE 669
//*                                                                 *   FILE 669
//*        RECEIVE the transport dataset, this will generate        *   FILE 669
//*        a pds with all neccessary members.                       *   FILE 669
//*        Edit and excute the $$$$EDIT member to update            *   FILE 669
//*        library names throughout the CBT library.                *   FILE 669
//*        Review and run the program member. This will             *   FILE 669
//*        install and verify the program.                          *   FILE 669
//*        You may edit and execute member Z669UPDT to update       *   FILE 669
//*        librarynames etc in the install lib.                     *   FILE 669
//*                                                                 *   FILE 669
//*       ISPDPX01 description                                      *   FILE 669
//*                                                                 *   FILE 669
//*        This  ISPF panel  exit is  used to  insert records       *   FILE 669
//*        into  an ISPF  panel.  It can  replace the  entire       *   FILE 669
//*        panel, or one  or more sections with  data in REXX       *   FILE 669
//*        stem variable(s).                                        *   FILE 669
//*        See member ISX1DOC for full  documentation.              *   FILE 669
//*        Members ISX1* are part of the ISPDPX01 package.          *   FILE 669
//*                                                                 *   FILE 669
//*       ISPPDA description                                        *   FILE 669
//*                                                                 *   FILE 669
//*        Panel using dynamic area to build scrollable display.    *   FILE 669
//*        Highlights                                               *   FILE 669
//*         -  Build and show the screen buffer                     *   FILE 669
//*         -  Update variables associated with input field areas.  *   FILE 669
//*         -  Calculate new top-of-panel pointer when scrolling    *   FILE 669
//*            request.                                             *   FILE 669
//*         -  Return a list of line commands with data pointer.    *   FILE 669
//*         -  Externalize panel display attribute characters.      *   FILE 669
//*                                                                 *   FILE 669
//*       REXXVARS description                                      *   FILE 669
//*                                                                 *   FILE 669
//*        REXXVARS is a general function to perform various        *   FILE 669
//*        actions for REXX variables - browse, copy, drop,         *   FILE 669
//*        edit, index, list, rename, sort and view. Some of        *   FILE 669
//*        those functions can be done using standard REXX          *   FILE 669
//*        features, though with some difficulties, others          *   FILE 669
//*        like index cannot. It can sort long variables (gt        *   FILE 669
//*        32756 bytes), which to the best of my knowledge no       *   FILE 669
//*        other sort can do.                                       *   FILE 669
//*        Multiple variable specifications can be entered          *   FILE 669
//*        as input, they can be a mixture of descrete names,       *   FILE 669
//*        masks or stems.                                          *   FILE 669
//*        The stack can be used as input and output for some       *   FILE 669
//*        functions.                                               *   FILE 669
//*        See member RXRVDOC for full  documentation.              *   FILE 669
//*        Members RXRV* are part of the REXXVARS package.          *   FILE 669
//*                                                                 *   FILE 669
//*       REXXGBLV description                                      *   FILE 669
//*                                                                 *   FILE 669
//*        Provides   a  variable   store  external   to  the       *   FILE 669
//*        currently running REXX program. REXX variables can       *   FILE 669
//*        be  copied to  the  external  store and  retrieved       *   FILE 669
//*        again at  some later time  by the same  or another       *   FILE 669
//*        REXX  process. The  saved  variables  can even  be       *   FILE 669
//*        written to and retrieved from  a disk file, so can       *   FILE 669
//*        be  used across  logons and  even be  shared among       *   FILE 669
//*        users.                                                   *   FILE 669
//*        Plus some REXX variable handling functions.              *   FILE 669
//*        See member RXGVDOC for full  documentation.              *   FILE 669
//*        See member RXGVRDME for a member list.                   *   FILE 669
//*        Members RXGV* are part of the REXXGBLV package.          *   FILE 669
//*                                                                 *   FILE 669
//*       REXXSTOR description                                      *   FILE 669
//*                                                                 *   FILE 669
//*        Allow a REXX program to  store a string of data in       *   FILE 669
//*        common storage and retrieve  it later, either from       *   FILE 669
//*        the  same program  or from  another REXX  program.       *   FILE 669
//*        See member RXSTDOC for full  documentation.              *   FILE 669
//*        Members RXST* are part of the REXXSTOR package.          *   FILE 669
//*                                                                 *   FILE 669
//*       RXHLLK description                                        *   FILE 669
//*                                                                 *   FILE 669
//*        Assembler subroutine to provide access for               *   FILE 669
//*        high-level programs to REXX services like                *   FILE 669
//*        variable get / put and the TSO stack, You can            *   FILE 669
//*        even start another REXX from the hi-level                *   FILE 669
//*        program. The module have an alias for C programs         *   FILE 669
//*        that use null-terminated strings.                        *   FILE 669
//*                                                                 *   FILE 669
//*       RXOPCOMM description                                      *   FILE 669
//*                                                                 *   FILE 669
//*        Allow MODIFY and STOP operator command for REXX          *   FILE 669
//*        programs (F jobname,some text, or P jobname).            *   FILE 669
//*        Issue WTO, optionally to be retained forever or          *   FILE 669
//*        till job end.                                            *   FILE 669
//*        See member RXOPDOC for full  documentation.              *   FILE 669
//*        Members RXOP* are part of the RXOPCOMM package.          *   FILE 669
//*                                                                 *   FILE 669
//*       RXPATTRN description                                      *   FILE 669
//*                                                                 *   FILE 669
//*        Test a string by a mask, return 0 if match.              *   FILE 669
//*        See member RXPNDOC for full  documentation.              *   FILE 669
//*        Members RXPN* are part of the RXPATTRN package.          *   FILE 669
//*                                                                 *   FILE 669
//*       RXPIPE description                                        *   FILE 669
//*                                                                 *   FILE 669
//*        RXPIPE executes a series of commands, called             *   FILE 669
//*        stages, passing the output of each stage as input        *   FILE 669
//*        to the next, through the TSO stack. In this it           *   FILE 669
//*        works similar to a MSDOS pipe. RXPIPE has a              *   FILE 669
//*        number of built-in transformers that manipulates         *   FILE 669
//*        the contents of the stack.                               *   FILE 669
//*                                                                 *   FILE 669
//*       RXRDPRML description                                      *   FILE 669
//*                                                                 *   FILE 669
//*        Read parmlib member, return data in stem.                *   FILE 669
//*        Some comments may be ignored.                            *   FILE 669
//*        See member RXRPDOC for full  documentation.              *   FILE 669
//*        Members RXRP* are part of the RXRDPRML package.          *   FILE 669
//*                                                                 *   FILE 669
//*       RXVSAMBA description                                      *   FILE 669
//*                                                                 *   FILE 669
//*        The program  can add, replace, retrieve  or delete       *   FILE 669
//*        records from a VSAM database. Acess is normally by       *   FILE 669
//*        key/keyprefix,  but  some functions  allow  access       *   FILE 669
//*        based on text anywhere in the record.                    *   FILE 669
//*        Data is either read from  a REXX stem or stored in       *   FILE 669
//*        a REXX stem.                                             *   FILE 669
//*        See member RXVBDOC for full  documentation.              *   FILE 669
//*        Members RXVB* are part of the RXVSAMBA package.          *   FILE 669
//*                                                                 *   FILE 669
//*       RXWAIT description                                        *   FILE 669
//*                                                                 *   FILE 669
//*        Wait whole seconds or fractions of a second.             *   FILE 669
//*        See member RXWTDOC for full  documentation.              *   FILE 669
//*        Members RXWT* are part of the RXWAIT package.            *   FILE 669
//*                                                                 *   FILE 669
//*       Other members of possible interest                        *   FILE 669
//*                                                                 *   FILE 669
//*        ISPXMACS  ASM copy book containing my macros for         *   FILE 669
//*                  interfacing with ISPF.                         *   FILE 669
//*        REXXMACS  ASM copy book containing my macros for         *   FILE 669
//*                  interfacing with REXX.                         *   FILE 669
//*        WSAMMACS  ASM copy book containing my structured         *   FILE 669
//*                  assembler macro set. WSAM is similar,          *   FILE 669
//*                  but not identical, to IBM's Structured         *   FILE 669
//*                  Programming Macros.                            *   FILE 669
//*                                                                 *   FILE 669
//*       Some notes                                                *   FILE 669
//*         Common macros devloped by me are combined in            *   FILE 669
//*         member SYSMACS. This member is included by the          *   FILE 669
//*         various products.                                       *   FILE 669
//*         Use member Z669UPDT to update JCL - if you have         *   FILE 669
//*         STARTOOL or PDS86 installed.                            *   FILE 669
//*                                                                 *   FILE 669
//*       Install notes                                             *   FILE 669
//*        -  Check member Z669MAC1, verify correct parameters      *   FILE 669
//*           for the generated job statements.                     *   FILE 669
//*        -  Check member Z669UPDT, update the LINKLIB and         *   FILE 669
//*           LPALIB value as needed.                               *   FILE 669
//*        -  Execute member Z669UPDT to update values in the       *   FILE 669
//*           library.                                              *   FILE 669
//*                                                                 *   FILE 669
```
