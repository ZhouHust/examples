# SCons build file for the various programs
# Run this typing 'scons'
# Clean the program by 'scons -c' (i.e., remove object, module and executable)

import os, sys

env_normal=Environment(ENV=os.environ)
env_lapack=Environment(ENV=os.environ)
env_mpi=Environment(ENV=os.environ,F90='mpif90',F90LINKER='mpif90')

# Assume that gfortran will be used. 
#Tool('gfortran')(env_normal)
#Tool('mpif90')(env_mpi)
#MY_F90FLAGS='-O2 -finline-functions -funswitch-loops -fwhole-file'
MY_F90FLAGS='-fdefault-real-8 -fall-intrinsics -std=f2008 -Wall'
MY_LINKFLAGS=''
LAPACK_LINKFLAGS='-L/opt/local/lib/lapack -llapack'

env_normal.Append(F90FLAGS=MY_F90FLAGS,LINKFLAGS=MY_LINKFLAGS,FORTRANMODDIRPREFIX='-J',FORTRANMODDIR = '${TARGET.dir}',F90PATH='${TARGET.dir}')
env_lapack.Append(F90FLAGS=MY_F90FLAGS,LINKFLAGS=LAPACK_LINKFLAGS,FORTRANMODDIRPREFIX='-J',FORTRANMODDIR = '${TARGET.dir}',F90PATH='${TARGET.dir}')
env_mpi.Append(F90FLAGS=MY_F90FLAGS,LINKFLAGS=MY_LINKFLAGS,FORTRANMODDIRPREFIX='-J',FORTRANMODDIR = '${TARGET.dir}',F90PATH='${TARGET.dir}')

variants={}
variants['build_initialize']       = (['initialize.f90','initialize_module.f90','utility_module.f90'],env_normal)
variants['build_mc_nvt_lj']        = (['mc_nvt_lj.f90','mc_lj_module.f90','utility_module.f90'],env_normal)
variants['build_mc_npt_lj']        = (['mc_npt_lj.f90','mc_lj_module.f90','utility_module.f90'],env_normal)
variants['build_mc_zvt_lj']        = (['mc_zvt_lj.f90','mc_lj_module.f90','utility_module.f90'],env_normal)
variants['build_md_nve_hs']        = (['md_nve_hs.f90','md_nve_hs_module.f90','utility_module.f90'],env_normal)
variants['build_mc_nvt_hs']        = (['mc_nvt_hs.f90','mc_hs_module.f90','utility_module.f90'],env_normal)
variants['build_mc_nvt_sc']        = (['mc_nvt_sc.f90','mc_sc_module.f90','utility_module.f90'],env_normal)
variants['build_md_nve_lj']        = (['md_nve_lj.f90','md_lj_module.f90','utility_module.f90'],env_normal)
variants['build_md_nve_lj_vl']     = (['md_nve_lj.f90','md_lj_vl_module.f90','verlet_list_module.f90','utility_module.f90'],env_normal)
variants['build_md_nve_lj_ll']     = (['md_nve_lj.f90','md_lj_ll_module.f90','link_list_module.f90','utility_module.f90'],env_normal)
variants['build_md_nvt_lj_le']     = (['md_nvt_lj_le.f90','md_lj_le_module.f90','utility_module.f90'],env_normal)
variants['build_md_nvt_lj_llle']   = (['md_nvt_lj_le.f90','md_lj_llle_module.f90','link_list_module.f90','utility_module.f90'],env_normal)
variants['build_mc_nvt_lj_ll']     = (['mc_nvt_lj.f90','mc_lj_ll_module.f90','link_list_module.f90','utility_module.f90'],env_normal)
variants['build_mc_npt_lj_ll']     = (['mc_npt_lj.f90','mc_lj_ll_module.f90','link_list_module.f90','utility_module.f90'],env_normal)
variants['build_mc_zvt_lj_ll']     = (['mc_zvt_lj.f90','mc_lj_ll_module.f90','link_list_module.f90','utility_module.f90'],env_normal)
variants['build_cluster']          = (['cluster.f90','utility_module.f90'],env_normal)
variants['build_diffusion']        = (['diffusion.f90'],env_normal)
variants['build_mesh']             = (['mesh.f90'],env_normal)
variants['build_test_pot_at']      = (['test_pot_atom.f90','test_pot_at.f90','utility_module.f90'],env_normal)
variants['build_test_pot_bend']    = (['test_pot_atom.f90','test_pot_bend.f90','utility_module.f90'],env_normal)
variants['build_test_pot_twist']   = (['test_pot_atom.f90','test_pot_twist.f90','utility_module.f90'],env_normal)
variants['build_test_pot_dd']      = (['test_pot_linear.f90','test_pot_dd.f90','utility_module.f90'],env_normal)
variants['build_test_pot_dq']      = (['test_pot_linear.f90','test_pot_dq.f90','utility_module.f90'],env_normal)
variants['build_test_pot_qq']      = (['test_pot_linear.f90','test_pot_qq.f90','utility_module.f90'],env_normal)
variants['build_test_pot_gb']      = (['test_pot_linear.f90','test_pot_gb.f90','utility_module.f90'],env_normal)
variants['build_md_chain']         = (['md_chain.f90','md_chain_module.f90','utility_module.f90'],env_lapack)

# Build each variant in appropriate variant directory
for variant_dir,(sources,env) in variants.iteritems():
    SConscript('SConscript', variant_dir=variant_dir,exports={'env':env,'sources':sources},duplicate=1)
