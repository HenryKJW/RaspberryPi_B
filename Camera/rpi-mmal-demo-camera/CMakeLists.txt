cmake_minimum_required(VERSION 2.8)

SET(COMPILE_DEFINITIONS -Werror)

include_directories(/opt/vc/include)
include_directories(/opt/vc/include/interface/vcos/pthreads)
include_directories(/opt/vc/include/interface/vmcs_host)
include_directories(/opt/vc/include/interface/vmcs_host/linux)

include_directories(/home/pi/git_server/Camera/userland)
include_directories(/opt/vc/src/hello_pi/libs/vgfont)

include_directories(/home/pi/git_server/Camera/rpi-mmal-demo-camera/MPU6050)
include_directories(/home/pi/git_server/Camera/rpi-mmal-demo-camera/Widget)

link_directories(/opt/vc/lib)
link_directories(/opt/vc/src/hello_pi/libs/vgfont)

link_directories(/home/pi/git_server/Camera/rpi-mmal-demo-camera/MPU6050)
link_directories(/home/pi/git_server/Camera/rpi-mmal-demo-camera/Widget)

add_executable(mmaldemo main.c)
add_executable(mmal_buffer_demo buffer_demo.c)
add_executable(mmal_opencv_demo opencv_demo.c)
add_executable(mmal_video_record video_record.c)

find_package( OpenCV REQUIRED )


target_link_libraries(mmaldemo mmal_core mmal_util mmal_vc_client vcos bcm_host)
target_link_libraries(mmal_buffer_demo mmal_core mmal_util mmal_vc_client vcos bcm_host rt)
target_link_libraries(mmal_opencv_demo mmal_core mmal_util mmal_vc_client vcos bcm_host ${OpenCV_LIBS} vgfont openmaxil EGL  pthread rt m freetype  mpu6050 mpu6050widget)
target_link_libraries(mmal_video_record mmal_core mmal_util mmal_vc_client vcos bcm_host cairo rt)
