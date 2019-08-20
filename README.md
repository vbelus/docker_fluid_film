# docker_fluid_film
An explanation as to how I created the docker image to launch trainings of my drl model

# Get started
You need docker to get started, if you're not familiar with it, check the official documentation here https://docs.docker.com/get-started/

# We start from an Ubuntu image
```
~$ docker pull ubuntu
```

# Then we create a container from the image
```
~$ docker run -ti --name drl_fluid_film ubuntu
root@4d11781e476d:/# exit
exit
```
You can see it, unused, with - $docker ps -a
```
~$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                          PORTS               NAMES
4d11781e476d        ubuntu              "/bin/bash"         About a minute ago   Exited (0) About a minute ago                       drl_fluid_film
```

# We start the container
```
~$ docker start drl_fluid_film
drl_fluid_film
```

And you can see it, active, with - $docker ps
```
~$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
4d11781e476d        ubuntu              "/bin/bash"         4 minutes ago       Up 2 seconds                            drl_fluid_film
```

# We can then open terminals inside the container with - $docker exec -ti drl_fluid_film /bin/bash -l
```
~$ docker exec -ti drl_fluid_film /bin/bash -l
root@4d11781e476d:/# 
```
# Packages I installed step by step
$apt-get update
```
root@4d11781e476d:/# apt-get update     
...
Fetched 17.0 MB in 3s (6386 kB/s)                          
Reading package lists... Done
```

$apt-get install python3
```
root@4d11781e476d:/# apt-get install python3
...
```
$apt-get install python3-pip python3-tk libopenmpi-dev wget libsm6 libxext6 libxrender-dev
```
root@4d11781e476d:/# apt-get install python3-pip python3-tk libopenmpi-dev wget libsm6 libxext6 libxrender-dev
...
done.
```

I now need to clone the repo in which the drl model is
$apt-get install git
```
root@4d11781e476d:/# apt-get install git
...
```

$cd
$git clone https://github.com/vbelus/drl_film_fluid
```
root@4d11781e476d:/# cd
root@4d11781e476d:~# git clone https://github.com/vbelus/drl_film_fluid
Cloning into 'drl_film_fluid'...
Username for 'https://github.com': vbelus
Password for 'https://vbelus@github.com': 
remote: Enumerating objects: 74, done.
remote: Counting objects: 100% (74/74), done.
remote: Compressing objects: 100% (54/54), done.
remote: Total 226 (delta 20), reused 56 (delta 15), pack-reused 152
Receiving objects: 100% (226/226), 33.58 MiB | 2.45 MiB/s, done.
Resolving deltas: 100% (35/35), done.
```

```
root@4d11781e476d:~# ls
drl_film_fluid
```

We install all the python dependencies of the project which are in setup.py
$cd ~/drl_film_fluid/drl_fluid_film_python3/gym-film
$pip3 install -e ./
```
root@4d11781e476d:~/drl_film_fluid/drl_fluid_film_python3/gym-film# pip3 install -e ./
Obtaining file:///root/drl_film_fluid/drl_fluid_film_python3/gym-film
...
Successfully installed PySimpleGUI-4.2.0 absl-py-0.7.1 astor-0.8.0 cloudpickle-1.2.1 cycler-0.10.0 future-0.17.1 gast-0.2.2 google-pasta-0.1.7 grpcio-1.23.0 gym-0.14.0 gym-film h5py-2.9.0 joblib-0.13.2 keras-applications-1.0.8 keras-preprocessing-1.1.0 kiwisolver-1.1.0 markdown-3.1.1 matplotlib-3.1.1 mpi4py-3.0.2 numpy-1.17.0 opencv-python-4.1.0.25 pandas-0.25.0 protobuf-3.9.1 pyglet-1.3.2 pyparsing-2.4.2 python-dateutil-2.8.0 pytz-2019.2 scipy-1.3.1 stable-baselines-2.7.0 tensorboard-1.14.0 tensorflow-1.14.0 tensorflow-estimator-1.14.0 termcolor-1.1.0 werkzeug-0.15.5 wrapt-1.11.2
```

We now get the boost library, we will install it in /usr/local/
$cd /usr/local
$wget -4 https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.bz2
```
root@4d11781e476d:/usr/local# wget -4 https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.bz2
--2019-08-20 17:47:28--  https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.bz2
...
boost_1_67_0.tar.bz2                               100%[================================================================================================================>]  83.29M  8.04MB/s    in 10s     

2019-08-20 17:47:38 (8.04 MB/s) - 'boost_1_67_0.tar.bz2' saved [87336566/87336566]
```

$tar --bzip2 -xf boost_1_67_0.tar.bz2 
```
root@4d11781e476d:/usr/local# tar --bzip2 -xf boost_1_67_0.tar.bz2 
```

We need to acquire the boost_python library
$cd boost_1_67_0
$./bootstrap.sh --with-libraries=python --with-python=python3.6
$./b2
```
root@4d11781e476d:/usr/local/boost_1_67_0# ./bootstrap.sh --with-libraries=python --with-python=python3.6
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
...

root@4d11781e476d:/usr/local/boost_1_67_0# ./b2
...
...updated 93 targets...


The Boost C++ Libraries were successfully built!

The following directory should be added to compiler include paths:

    /usr/local/boost_1_67_0

The following directory should be added to linker library paths:

    /usr/local/boost_1_67_0/stage/lib
```

You need to let the linker know the path to the library libboost_numpy36.so.1.67.0
$export LD_LIBRARY_PATH=/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi:$LD_LIBRARY_PATH
```
root@4d11781e476d:~/drl_film_fluid/drl_fluid_film_python3/gym-film# export LD_LIBRARY_PATH=/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi:$LD_LIBRARY_PATH
```

Now we need to make sure the python/cpp bridge in our simulation solver is well built
$cd ~/drl_film_fluid/drl_fluid_film_python3/gym-film/gym_film/envs/simulation_solver
$make clean
$make
```
root@4d11781e476d:~/drl_film_fluid/drl_fluid_film_python3/gym-film/gym_film/envs/simulation_solver# make clean
rm simulation_cpp.o advect_in_time.o TVD3.o cpp.so
rm: cannot remove 'cpp.so': No such file or directory
makefile:21: recipe for target 'clean' failed
make: *** [clean] Error 1
root@4d11781e476d:~/drl_film_fluid/drl_fluid_film_python3/gym-film/gym_film/envs/simulation_solver# make
g++ -fPIC -o simulation_cpp.o -c simulation_cpp.cpp -I/usr/include/python3.6 -I/usr/local/boost_1_67_0 -I/usr/local/boost_1_67_0/stage/lib -I/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi -std=c++11 -Ofast -march=native -flto
In file included from /usr/local/boost_1_67_0/boost/python/detail/is_xxx.hpp:8:0,
                 from /usr/local/boost_1_67_0/boost/python/detail/is_auto_ptr.hpp:9,
                 from /usr/local/boost_1_67_0/boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from /usr/local/boost_1_67_0/boost/python/detail/value_arg.hpp:7,
                 from /usr/local/boost_1_67_0/boost/python/object/forward.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python/object/pointer_holder.hpp:16,
                 from /usr/local/boost_1_67_0/boost/python/to_python_indirect.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python/converter/arg_to_python.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python/call.hpp:15,
                 from /usr/local/boost_1_67_0/boost/python/object_core.hpp:14,
                 from /usr/local/boost_1_67_0/boost/python/args.hpp:22,
                 from /usr/local/boost_1_67_0/boost/python.hpp:11,
                 from simulation_cpp.cpp:1:
/usr/local/boost_1_67_0/boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
/usr/local/boost_1_67_0/boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
/usr/local/boost_1_67_0/boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from /usr/local/boost_1_67_0/boost/function/function_base.hpp:16,
                 from /usr/local/boost_1_67_0/boost/function/detail/prologue.hpp:17,
                 from /usr/local/boost_1_67_0/boost/function/function_template.hpp:13,
                 from /usr/local/boost_1_67_0/boost/function/detail/maybe_include.hpp:15,
                 from /usr/local/boost_1_67_0/boost/function/function0.hpp:11,
                 from /usr/local/boost_1_67_0/boost/python/errors.hpp:13,
                 from /usr/local/boost_1_67_0/boost/python/handle.hpp:11,
                 from /usr/local/boost_1_67_0/boost/python/args_fwd.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python/args.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python.hpp:11,
                 from simulation_cpp.cpp:1:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
g++ -fPIC -o TVD3.o -c TVD3.cpp -I/usr/include/python3.6 -I/usr/local/boost_1_67_0 -I/usr/local/boost_1_67_0/stage/lib -I/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi -std=c++11 -Ofast -march=native -flto
g++ -fPIC -o advect_in_time.o -c advect_in_time.cpp -I/usr/include/python3.6 -I/usr/local/boost_1_67_0 -I/usr/local/boost_1_67_0/stage/lib -I/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi -std=c++11 -Ofast -march=native -flto
g++ -shared -o cpp.so simulation_cpp.o TVD3.o advect_in_time.o -L/usr/local/boost_1_67_0/stage/lib -lpython3.6m -lboost_numpy36 -std=c++11 -Ofast -march=native -flto
```
That's it, the environment is ready for trainings !
