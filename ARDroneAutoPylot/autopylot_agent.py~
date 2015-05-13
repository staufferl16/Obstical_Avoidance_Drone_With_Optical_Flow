#!/usr/bin/python

# We scale the image down for faster processing
SCALEDOWN = 2

import numpy as np

from optical_flow import OpticalFlowCalculator

# Routine called by C program.
def action(img_bytes, img_width, img_height, is_belly, ctrl_state, vbat_flying_percentage, theta, phi, psi, altitude, vx, vy):

    # Set up command defaults
    zap = 0
    phi = 0     
    theta = 0
    gaz = 0
    yaw = 0

    # Set up state variables first time around.  This is a cheap way of mocking up a Python
    # class __init__() method.
    if not hasattr(action, 'flowCalc'):

        action.flowCalc = OpticalFlowCalculator(640/SCALEDOWN,360/SCALEDOWN, window_name='OpticalFlow', battery = vbat_flying_percentage)

	print("!"*10)
	print(action.flowCalc.magnitude)
                
    # Create full-color image from bytes
    image = np.frombuffer(img_bytes, np.uint8)
    image = np.reshape(image, (img_height,img_width,3))
                    
    # Compute optical flow from image
    action.flowCalc.processFrame(image)

    # Send control parameters back to drone
    return (zap, phi, theta, gaz, yaw)
