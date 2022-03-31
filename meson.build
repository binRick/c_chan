#//***********************************************************/
project(
    'c_chan',          ['c'],         version : '0.0.1',         
    default_options : ['warning_level=2','c_std=gnu99'],
)
#//***********************************************************/
host_system = host_machine.system()

cc = meson.get_compiler('c')
sh = find_program('sh', required : true)
passh = find_program('passh', required : true)

#//***********************************************************/
test_deps = []
#//***********************************************************/
incdir = include_directories(
  './include', 
  './src', 
  './deps', 
  '../',
  '../metalang99/include',
  '../ok',
)
#//***********************************************************/
test_script1 = executable('test_script1', [ 
    'deps/c_scriptexec/example.c',
  ], include_directories : [incdir], 
  dependencies : [],
)
test_chan2 = executable('test_chan2', [ 
    'tests/test_chan2.c',  
    'src/fsio.c',
  ], include_directories : [incdir], 
  dependencies : [],
)
test_chan1 = executable('test_chan1', [ 
    'tests/test_chan1.c',  
    'src/fsio.c',
  ], include_directories : [incdir], 
  dependencies : [],
)
#//***********************************************************/
tests = [
  ['test chan 1', test_chan1, 'test-chan-1.log'],
  ['test chan 1', test_chan2, 'test-chan-1.log'],
  #/  ['script 1', test_script1, 'test-script-1.log'],
]
#//***********************************************************/

#//***********************************************************/
test_env = environment()
test_env.set('__SH', sh.full_path())
test_env.set('__BD', meson.current_build_dir())
test_env.set('__SD', meson.current_source_dir())
#//***********************************************************/
foreach i : tests
test(i[0], passh, args: ['-L', i[2], i[1] ], env: test_env)
endforeach
#//***********************************************************/


