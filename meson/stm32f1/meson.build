project('stm32f1-project', 'cpp')

size = find_program('arm-none-eabi-size')
objcopy = find_program('arm-none-eabi-objcopy')
stinfo = find_program('st-info')
stflash = find_program('st-flash')

#define libopencm3 path here
libocm3Path = '/home/ami/repos/libopencm3'

#define cpu types here
cputype = 'cortex-m3'
cpudefine = 'STM32F1'
libocm3cputype = 'opencm3_stm32f1'

#Add your source files here
srcfiles = ['blink.cpp']


libocm3IncPath = libocm3Path + '/include'
libocm3LibPath = libocm3Path + '/lib'

stm32f1cargs = ['-Os',
                '-ggdb',
                '-mcpu=' + cputype,
                '-mthumb',
                '-mthumb-interwork',
                '-msoft-float',
                '-std=gnu++14',
                '-Wall',
                '-ffunction-sections',
                '-fdata-sections',
                '-D' + cpudefine,
                '-fdata-sections',
                '-fno-exceptions',
                '-I' + libocm3IncPath
                ]

stm32f1linkargs = ['-Os',
                '-ggdb',
                '-D' + cpudefine,
                '-fdata-sections',
                '-mcpu=' + cputype,
                '-mthumb',
                '-mthumb-interwork',
                '-msoft-float',
                '-lc',
                '-flto',
                '-T../libopencm3_f1.ld',
                '--specs=nosys.specs',
                '-nostartfiles',
                '-Wl,--gc-sections',
                '-Wl,--gc-sections',
                '-Wl,--relax',
                '-L' + libocm3LibPath,
                '-l' + libocm3cputype,
                 ]

p = ['blink', srcfiles, stm32f1cargs, stm32f1linkargs]

exe = executable(p[0], p[1],
                 cpp_args: p[2],
                 link_args: p[3],
                 build_by_default: true)

run_target('hex', command: [objcopy, ['-Obinary', exe.full_path(),
           exe.full_path() + '.hex']], depends: exe)
run_target('size', command: [size, exe.full_path(), '-B'], depends: exe)

# STlink programmer related commands
run_target('probe', command: [stinfo, '--probe'])
run_target('upload', command: [stflash, 'write', exe.full_path() + '.hex', '0x08000000'], depends: exe)
