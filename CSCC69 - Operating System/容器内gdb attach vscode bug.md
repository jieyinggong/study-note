---
tags:
  - bug
---


```
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (63) LaunchOptions{\"name\":\"Pintos debug\",\"type\":\"cppdbg\",\"request\":\"launch\",\"program\":\"/pintos/src/threads/build/kernel.o\",\"additionalSOLibSearchPath\":\"/pintos/src/threads/build\",\"cwd\":\"/pintos\",\"MIMode\":\"gdb\",\"miDebuggerPath\":\"/usr/bin/gdb\",\"miDebuggerArgs\":\"-x /pintos/src/misc/gdb-macros\",\"logging\":{\"trace\":true,\"traceResponse\":true,\"engineLogging\":true},\"launchCompleteCommand\":\"exec-continue\",\"setupCommands\":[{\"description\":\"Enable asynchronous MI output\",\"text\":\"-gdb-set mi-async on\",\"ignoreFailures\":false},{\"description\":\"Load Pintos kernel symbols\",\"text\":\"-file-exec-and-symbols /pintos/src/threads/build/kernel.o\",\"ignoreFailures\":false},{\"description\":\"Connect to remote GDB stub\",\"text\":\"-target-select remote localhost:1234\",\"ignoreFailures\":false},{\"text\":\"-break-insert main\"},{\"description\":\"Enable pretty-printing\",\"text\":\"-enable-pretty-printing\",\"ignoreFailures\":true},{\"text\":\"-break-insert init.c:90\"}],\"__configurationTarget\":6,\"__sessionId\":\"ff750ae5-8e68-42f9-8683-6a2bace172fd\"}\n"},"seq":2}
1: (63) LaunchOptions{"name":"Pintos debug","type":"cppdbg","request":"launch","program":"/pintos/src/threads/build/kernel.o","additionalSOLibSearchPath":"/pintos/src/threads/build","cwd":"/pintos","MIMode":"gdb","miDebuggerPath":"/usr/bin/gdb","miDebuggerArgs":"-x /pintos/src/misc/gdb-macros","logging":{"trace":true,"traceResponse":true,"engineLogging":true},"launchCompleteCommand":"exec-continue","setupCommands":[{"description":"Enable asynchronous MI output","text":"-gdb-set mi-async on","ignoreFailures":false},{"description":"Load Pintos kernel symbols","text":"-file-exec-and-symbols /pintos/src/threads/build/kernel.o","ignoreFailures":false},{"description":"Connect to remote GDB stub","text":"-target-select remote localhost:1234","ignoreFailures":false},{"text":"-break-insert main"},{"description":"Enable pretty-printing","text":"-enable-pretty-printing","ignoreFailures":true},{"text":"-break-insert init.c:90"}],"__configurationTarget":6,"__sessionId":"ff750ae5-8e68-42f9-8683-6a2bace172fd"}
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (97) DbgCmd:echo $$ > /tmp/Microsoft-MIEngine-Pid-oejdxv1d.4am ; cd \"/pintos/src/threads/build\" ; DbgTerm=`tty` ; set -o monitor ; trap 'rm \"/tmp/Microsoft-MIEngine-In-m4cukgl2.ahw\" \"/tmp/Microsoft-MIEngine-Out-l31v4hed.cni\" \"/tmp/Microsoft-MIEngine-Pid-oejdxv1d.4am\" \"/tmp/Microsoft-MIEngine-Cmd-dib3kb1r.bck\"' EXIT ; \"/usr/bin/gdb\" --interpreter=mi -x /pintos/src/misc/gdb-macros --tty=$DbgTerm < \"/tmp/Microsoft-MIEngine-In-m4cukgl2.ahw\" > \"/tmp/Microsoft-MIEngine-Out-l31v4hed.cni\" & clear; pid=$! ; echo $pid > \"/tmp/Microsoft-MIEngine-Pid-oejdxv1d.4am\" ; wait $pid; \n"},"seq":4}
1: (97) DbgCmd:echo $$ > /tmp/Microsoft-MIEngine-Pid-oejdxv1d.4am ; cd "/pintos/src/threads/build" ; DbgTerm=`tty` ; set -o monitor ; trap 'rm "/tmp/Microsoft-MIEngine-In-m4cukgl2.ahw" "/tmp/Microsoft-MIEngine-Out-l31v4hed.cni" "/tmp/Microsoft-MIEngine-Pid-oejdxv1d.4am" "/tmp/Microsoft-MIEngine-Cmd-dib3kb1r.bck"' EXIT ; "/usr/bin/gdb" --interpreter=mi -x /pintos/src/misc/gdb-macros --tty=$DbgTerm < "/tmp/Microsoft-MIEngine-In-m4cukgl2.ahw" > "/tmp/Microsoft-MIEngine-Out-l31v4hed.cni" & clear; pid=$! ; echo $pid > "/tmp/Microsoft-MIEngine-Pid-oejdxv1d.4am" ; wait $pid;
--> C (runInTerminal-6): {"type":"request","command":"runInTerminal","arguments":{"kind":"integrated","title":"cppdbg: kernel.o","cwd":"","args":["/bin/sh","/tmp/Microsoft-MIEngine-Cmd-dib3kb1r.bck"],"env":{}},"seq":6}
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (105) Wait for connection completion.\n"},"seq":8}
1: (105) Wait for connection completion.
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (534) ->=thread-group-added,id=\"i1\"\n"},"seq":10}
1: (534) ->=thread-group-added,id="i1"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (542) ->~\"GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1\\n\"\n"},"seq":12}
1: (542) ->~"GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (543) ->~\"Copyright (C) 2022 Free Software Foundation, Inc.\\n\"\n"},"seq":14}
1: (543) ->~"Copyright (C) 2022 Free Software Foundation, Inc.\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (543) ->~\"License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>\\nThis is free software: you are free to change and redistribute it.\\nThere is NO WARRANTY, to the extent permitted by law.\"\n"},"seq":16}
1: (543) ->~"License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>\nThis is free software: you are free to change and redistribute it.\nThere is NO WARRANTY, to the extent permitted by law."
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (543) ->~\"\\nType \\\"show copying\\\" and \\\"show warranty\\\" for details.\\n\"\n"},"seq":18}
1: (543) ->~"\nType \"show copying\" and \"show warranty\" for details.\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->~\"This GDB was configured as \\\"x86_64-linux-gnu\\\".\\n\"\n"},"seq":20}
1: (544) ->~"This GDB was configured as \"x86_64-linux-gnu\".\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->~\"Type \\\"show configuration\\\" for configuration details.\\n\"\n"},"seq":22}
1: (544) ->~"Type \"show configuration\" for configuration details.\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->~\"For bug reporting instructions, please see:\\n\"\n"},"seq":24}
1: (544) ->~"For bug reporting instructions, please see:\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->~\"<https://www.gnu.org/software/gdb/bugs/>.\\n\"\n"},"seq":26}
1: (544) ->~"<https://www.gnu.org/software/gdb/bugs/>.\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->~\"Find the GDB manual and other documentation resources online at:\\n    <http://www.gnu.org/software/gdb/documentation/>.\"\n"},"seq":28}
1: (544) ->~"Find the GDB manual and other documentation resources online at:\n    <http://www.gnu.org/software/gdb/documentation/>."
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->~\"\\n\\n\"\n"},"seq":30}
1: (544) ->~"\n\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->~\"For help, type \\\"help\\\".\\n\"\n"},"seq":32}
1: (544) ->~"For help, type \"help\".\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->~\"Type \\\"apropos word\\\" to search for commands related to \\\"word\\\".\\n\"\n"},"seq":34}
1: (544) ->~"Type \"apropos word\" to search for commands related to \"word\".\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (544) ->(gdb)\n"},"seq":36}
1: (544) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (548) <-1001-gdb-set mi-async on\n"},"seq":38}
1: (548) <-1001-gdb-set mi-async on
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (549) ->1001^done\n"},"seq":40}
1: (549) ->1001^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (549) ->(gdb)\n"},"seq":42}
1: (549) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (551) 1001: elapsed time 3\n"},"seq":44}
1: (551) 1001: elapsed time 3
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (556) <-1002-gdb-set mi-async on\n"},"seq":46}
1: (556) <-1002-gdb-set mi-async on
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (557) ->1002^done\n"},"seq":48}
1: (557) ->1002^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (557) ->(gdb)\n"},"seq":50}
1: (557) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (557) 1002: elapsed time 0\n"},"seq":52}
1: (557) 1002: elapsed time 0
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (557) <-1003-file-exec-and-symbols /pintos/src/threads/build/kernel.o\n"},"seq":54}
1: (557) <-1003-file-exec-and-symbols /pintos/src/threads/build/kernel.o
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (589) ->1003^done\n"},"seq":56}
1: (589) ->1003^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (590) ->(gdb)\n"},"seq":58}
1: (590) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (590) 1003: elapsed time 32\n"},"seq":60}
1: (590) 1003: elapsed time 32
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (590) <-1004-target-select remote localhost:1234\n"},"seq":62}
1: (590) <-1004-target-select remote localhost:1234
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (972) ->=thread-group-started,id=\"i1\",pid=\"42000\"\n"},"seq":64}
1: (972) ->=thread-group-started,id="i1",pid="42000"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (981) ->=thread-created,id=\"1\",group-id=\"i1\"\n"},"seq":66}
1: (981) ->=thread-created,id="1",group-id="i1"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (988) <-1005-thread-info 1\n"},"seq":68}
1: (988) <-1005-thread-info 1
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1337) ->~\"0x0000fff0 in ?? ()\\n\"\n"},"seq":70}
1: (1337) ->~"0x0000fff0 in ?? ()\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1339) ->*stopped,frame={addr=\"0x0000fff0\",func=\"??\",args=[],arch=\"i386\"},thread-id=\"1\",stopped-threads=\"all\"\n"},"seq":72}
1: (1339) ->*stopped,frame={addr="0x0000fff0",func="??",args=[],arch="i386"},thread-id="1",stopped-threads="all"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1378) ->1004^connected\n"},"seq":74}
1: (1378) ->1004^connected
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1378) ->(gdb)\n"},"seq":76}
1: (1378) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1379) 1004: elapsed time 788\n"},"seq":78}
1: (1379) 1004: elapsed time 788
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1379) <-1006-break-insert main\n"},"seq":80}
1: (1379) <-1006-break-insert main
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1583) ->1005^done,threads=[{id=\"1\",target-id=\"Thread <main>\",frame={level=\"0\",addr=\"0x0000fff0\",func=\"??\",args=[],arch=\"i386\"},state=\"stopped\"}]\n"},"seq":82}
1: (1583) ->1005^done,threads=[{id="1",target-id="Thread <main>",frame={level="0",addr="0x0000fff0",func="??",args=[],arch="i386"},state="stopped"}]
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1585) ->(gdb)\n"},"seq":84}
1: (1585) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1586) 1005: elapsed time 597\n"},"seq":86}
1: (1586) 1005: elapsed time 597
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1678) ->1006^done,bkpt={number=\"1\",type=\"breakpoint\",disp=\"keep\",enabled=\"y\",addr=\"0xc00203dc\",func=\"main\",file=\"../../threads/init.c\",fullname=\"/pintos/src/threads/init.c\",line=\"78\",thread-groups=[\"i1\"],times=\"0\",original-location=\"main\"}\n"},"seq":88}
1: (1678) ->1006^done,bkpt={number="1",type="breakpoint",disp="keep",enabled="y",addr="0xc00203dc",func="main",file="../../threads/init.c",fullname="/pintos/src/threads/init.c",line="78",thread-groups=["i1"],times="0",original-location="main"}
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1678) ->(gdb)\n"},"seq":90}
1: (1678) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1678) 1006: elapsed time 299\n"},"seq":92}
1: (1678) 1006: elapsed time 299
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1678) <-1007-enable-pretty-printing\n"},"seq":94}
1: (1678) <-1007-enable-pretty-printing
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1679) ->1007^done\n"},"seq":96}
1: (1679) ->1007^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1684) ->(gdb)\n"},"seq":98}
1: (1684) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1684) 1007: elapsed time 6\n"},"seq":100}
1: (1684) 1007: elapsed time 6
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1685) <-1008-break-insert init.c:90\n"},"seq":102}
1: (1685) <-1008-break-insert init.c:90
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1729) ->1008^done,bkpt={number=\"2\",type=\"breakpoint\",disp=\"keep\",enabled=\"y\",addr=\"0xc0020414\",func=\"main\",file=\"../../threads/init.c\",fullname=\"/pintos/src/threads/init.c\",line=\"90\",thread-groups=[\"i1\"],times=\"0\",original-location=\"init.c:90\"}\n"},"seq":104}
1: (1729) ->1008^done,bkpt={number="2",type="breakpoint",disp="keep",enabled="y",addr="0xc0020414",func="main",file="../../threads/init.c",fullname="/pintos/src/threads/init.c",line="90",thread-groups=["i1"],times="0",original-location="init.c:90"}
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1729) ->(gdb)\n"},"seq":106}
1: (1729) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1729) 1008: elapsed time 43\n"},"seq":108}
1: (1729) 1008: elapsed time 43
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1729) <-1009-interpreter-exec console \"set pagination off\"\n"},"seq":110}
1: (1729) <-1009-interpreter-exec console "set pagination off"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1729) ->=cmd-param-changed,param=\"pagination\",value=\"off\"\n"},"seq":112}
1: (1729) ->=cmd-param-changed,param="pagination",value="off"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1729) ->1009^done\n"},"seq":114}
1: (1729) ->1009^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1730) ->(gdb)\n"},"seq":116}
1: (1730) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1730) 1009: elapsed time 0\n"},"seq":118}
1: (1730) 1009: elapsed time 0
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1730) <-1010-gdb-set auto-solib-add on\n"},"seq":120}
1: (1730) <-1010-gdb-set auto-solib-add on
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1730) ->1010^done\n"},"seq":122}
1: (1730) ->1010^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1730) ->(gdb)\n"},"seq":124}
1: (1730) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1730) 1010: elapsed time 0\n"},"seq":126}
1: (1730) 1010: elapsed time 0
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1730) <-1011-gdb-set solib-search-path /pintos/src/threads/build:\n"},"seq":128}
1: (1730) <-1011-gdb-set solib-search-path /pintos/src/threads/build:
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1814) ->1011^done\n"},"seq":130}
1: (1814) ->1011^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1816) 1011: elapsed time 86\n"},"seq":132}
1: (1816) 1011: elapsed time 86
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1816) ->(gdb)\n"},"seq":134}
1: (1816) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1816) <-1012-gdb-set stop-on-solib-events 1\n"},"seq":136}
1: (1816) <-1012-gdb-set stop-on-solib-events 1
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1817) ->1012^done\n"},"seq":138}
1: (1817) ->1012^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1817) ->(gdb)\n"},"seq":140}
1: (1817) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1817) 1012: elapsed time 0\n"},"seq":142}
1: (1817) 1012: elapsed time 0
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1817) <-1013-environment-cd /pintos\n"},"seq":144}
1: (1817) <-1013-environment-cd /pintos
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1818) ->1013^done\n"},"seq":146}
1: (1818) ->1013^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1818) ->(gdb)\n"},"seq":148}
1: (1818) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1818) 1013: elapsed time 0\n"},"seq":150}
1: (1818) 1013: elapsed time 0
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1818) <-1014-file-exec-and-symbols /pintos/src/threads/build/kernel.o\n"},"seq":152}
1: (1818) <-1014-file-exec-and-symbols /pintos/src/threads/build/kernel.o
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1953) ->1014^done\n"},"seq":154}
1: (1953) ->1014^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1954) ->(gdb)\n"},"seq":156}
1: (1954) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1957) 1014: elapsed time 138\n"},"seq":158}
1: (1957) 1014: elapsed time 138
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1960) <-1015-interpreter-exec console \"show architecture\"\n"},"seq":160}
1: (1960) <-1015-interpreter-exec console "show architecture"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1961) ->~\"The target architecture is set to \\\"auto\\\" (currently \\\"i386\\\").\\n\"\n"},"seq":162}
1: (1961) ->~"The target architecture is set to \"auto\" (currently \"i386\").\n"
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1961) ->1015^done\n"},"seq":164}
1: (1961) ->1015^done
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1961) ->(gdb)\n"},"seq":166}
1: (1961) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1961) 1015: elapsed time 1\n"},"seq":168}
1: (1961) 1015: elapsed time 1
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (1963) <-1016-break-insert -f main\n"},"seq":170}
1: (1963) <-1016-break-insert -f main
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (2005) ->1016^done,bkpt={number=\"3\",type=\"breakpoint\",disp=\"keep\",enabled=\"y\",addr=\"0xc00203dc\",func=\"main\",file=\"../../threads/init.c\",fullname=\"/pintos/src/threads/init.c\",line=\"78\",thread-groups=[\"i1\"],times=\"0\",original-location=\"main\"}\n"},"seq":172}
1: (2005) ->1016^done,bkpt={number="3",type="breakpoint",disp="keep",enabled="y",addr="0xc00203dc",func="main",file="../../threads/init.c",fullname="/pintos/src/threads/init.c",line="78",thread-groups=["i1"],times="0",original-location="main"}
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (2005) ->(gdb)\n"},"seq":174}
1: (2005) ->(gdb)
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (2005) 1016: elapsed time 42\n"},"seq":176}
1: (2005) 1016: elapsed time 42
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (2014) Send Event AD7EngineCreateEvent\n"},"seq":178}
1: (2014) Send Event AD7EngineCreateEvent
--> E (output): {"type":"event","event":"output","body":{"category":"console","output":"1: (2016) Send Event AD7ProgramCreateEvent\n"},"seq":180}
1: (2016) Send Event AD7ProgramCreateEvent
--> E (output): {"type":"event","event":"output","body":{"category":"telemetry","output":"VS/Diagnostics/Debugger/Launch","data":{"VS.Diagnostics.Debugger.ImplementationName":"Microsoft.MIDebugEngine","VS.Diagnostics.Debugger.EngineVersion":"17.12.21003.1","VS.Diagnostics.Debugger.HostVersion":"17.12.21003.1","VS.Diagnostics.Debugger.AdapterId":"cppdbg","VS.Diagnostics.Debugger.Launch.Duration":1963,"VS.Diagnostics.Debugger.MIMode":"gdb","VS.Diagnostics.Debugger.FrameworkVersion":"8.0.824.36612"}},"seq":182}
--> R (launch-2): {"type":"response","request_seq":2,"success":true,"command":"launch","body":{},"seq":184}
Stopping due to fatal error: CustomAttributeFormatException: 'ReadData' property specified was not found.
```


太棒了，今天终于给我稳定抛出这一个error了....
感觉还是cpptool的插件哪里冲突了（

# 不知道有没有用的来自gpt o3的解决方案
下面这段 MIEngine 日志说明 **GDB 其实已经连上 QEMU-stub，并且两个断点都成功设下**——也就是说 Pintos / GDB / 端口 1234 都没问题。  
真正的炸点出现在 VS Code 的 **C/C++ 扩展（cppdbg 适配器）内部**：

```
Stopping due to fatal error:
CustomAttributeFormatException: 'ReadData' property specified was not found.
```

这条异常是 .NET 运行时在**反射解析调试协议对象的自定义特性**时抛出的。  
最近 1 ~ 2 个月里，有多位用户在 **cpptools ≥ 1.25.x** 版本、尤其是远程 / 容器 / Rosetta 场景下遇到同样的报错 ([Stack Overflow](https://stackoverflow.com/questions/79562623/vscode-gdb-debugging-fails-with-customattributeformatexception-when-using-rosett "c++ - VSCode GDB Debugging Fails with CustomAttributeFormatException When Using Rosetta - Stack Overflow"))。  
根因是：

- 1.25.x 开始默认启用新的 **原生（.NET 8）调试适配器**；
    
- 同时市场里仍可能残留旧版 **C/C++ Extension Pack** 或其他调试扩展，二者加载到同一进程后，反射到缺失的 `ReadData` 字段就会触发 `CustomAttributeFormatException`。
    

---

## 快速解决方案

| 方案                 | 操作                                                                                 | 代价        | 备注                                 |
| ------------------ | ---------------------------------------------------------------------------------- | --------- | ---------------------------------- |
| **回退到旧调试适配器（最省事）** | 在 `settings.json` 增加：`"C_Cpp.debugAdapter": "legacy"`                              | 0 min     | 立刻让扩展改用旧的 NodeJS 实现，规避 .NET 反射 bug |
| **换用稳定版 1.24.1**   | `code --install-extension ms-vscode.cpptools@1.24.1 --force`                       | 2 min     | 1.24.x 仍然使用旧适配器，不受影响               |
| **升级到每日 Insiders** | `code --install-extension ms-vscode.cpptools-insiders --force`                     | 2 min     | 本月 nightly 已合入补丁，若想继续用新适配器就选这个     |
| **清理冲突扩展**         | 1. 只保留 **“C/C++”** 主扩展2. 卸载 _C/C++ Extension Pack_、_Native Debug_、_Code-LLDB_ 之后再试 | 2 ~ 3 min | 如果只装一个 cppdbg，就不会混到旧 DLL           |

> **推荐路径**：先把 `"C_Cpp.debugAdapter": "legacy"` 打开验证确实不再 crash，再决定是降级还是升级 Insiders。

---

## 其他排查 Checklist

1. **容器端扩展目录**  
    复杂 reopen container 的过程可能留下一堆版本不一致的扩展副本，清理一下：
    
    ```bash
    rm -rf ~/.vscode-server/extensions/ms-vscode.cpptools*
    ```
    
    重新启动 VS Code 让它自动下最新版/指定版。
    
2. **launch.json 冗余字段**  
    你的配置里有两段 `-break-insert main` / `init.c:90`，理论上没问题，但可以把
    
    ```json
    "setupCommands": [...],
    "launchCompleteCommand": "exec-continue"
    ```
    
    简化为官方模版看看是否仍复现，以排除宏文件里输出“奇怪 JSON”干扰调试协议的可能。
    
3. **确认 dotnet 运行时**  
    如果你在 devcontainer 里手动装过旧版 `dotnet-6`，可能被新的 cpptools 调用。保证 `/usr/bin/dotnet --info` 输出的是 8.0+ 或干脆移除 dotnet，让扩展用自带 runtime。
    

---

## 临时替代方案

- 直接在 **VS Code 终端里手动 `gdb -x <macro>`**，配合 `monitor`, `continue`, `bt` 等命令。
    
- 或者装 **CodeLLDB**，用 lldb-MI 连接 `localhost:1234`，不依赖 cpptools 的 MIEngine。（Pintos i386 也能用 lldb-MI 调 QEMU stub）
    

---

### 小结

- **问题不在 Pintos / GDB，而在 VS Code C/C++ 扩展 1.25.x 的新调试适配器**。
    
- 最快的修复是 **切回 `"debugAdapter": "legacy"` 或降级到 1.24.1**；想继续用新适配器，就装 Insiders。
    
- 清理重复扩展、统一 dotnet 版本，可以避免未来更新时再次踩坑。
    

按上面步骤处理后，再运行 `pintos --gdb ...` + F5 理论上就能稳定进入断点了。如果还有别的异常，随时贴日志来继续排查。祝调通！


# 另一个插件冲突的样子

我选择放弃

```
2025-05-22 09:05:13.385 [info] [Window] Auto updating outdated extensions. ms-toolsai.jupyter, ms-vscode.cpptools

2025-05-22 09:05:14.387 [info] [Window] Auto update disabled for extension ms-vscode.cpptools

2025-05-22 09:05:14.387 [info] [Window] Auto updating extension ms-toolsai.jupyter

2025-05-22 09:05:14.509 [info] [Views] Added views:workbench.scm.history in workbench.view.scm

2025-05-22 09:05:16.456 [error] [Window] Cannot read the extension from /root/.vscode-server/extensions/ms-toolsai.jupyter-2025.4.1-linux-x64: ScanningExtension: Cannot read the extension from /root/.vscode-server/extensions/ms-toolsai.jupyter-2025.4.1-linux-x64

at Uh.scanLocalExtension (file:///vscode/vscode-server/bin/linux-x64/17baf841131aa23349f217ca7c570c76ee87b957/out/server-main.js:55:25161)

at async Fh.h (file:///vscode/vscode-server/bin/linux-x64/17baf841131aa23349f217ca7c570c76ee87b957/out/server-main.js:55:30402)

2025-05-22 09:05:22.870 [info] [Window] Extension host (Remote) is unresponsive.

2025-05-22 09:05:23.080 [info] [Window] Extension host (Remote) is responsive.
```



这些东西所以到底为什么昨天能突然连上啊啊啊啊
起码我现在log翻得很熟练了（