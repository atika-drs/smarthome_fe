<template>
    <section class="section section-shaped section-lg my-0">
        <div class="container pt-lg-md">
            <div class="row justify-content-center">
                <div id="app">
                    <div>
                        <base-button class="btn-1" outline type="primary" :class="{ 'is-primary' : !isCameraOpen, 'is-danger' : isCameraOpen}" @click="toggleCamera">
                            <span v-if="!isCameraOpen">Open Camera</span>
                            <span v-else>Close Camera</span>
                        </base-button>
                    </div>
                    
                    <!--div v-show="isCameraOpen && isLoading">
                        <ul class="loader-circle">
                            <li></li>
                            <li></li>
                            <li></li>
                        </ul>
                    </div-->
                    
                    <div v-if="isCameraOpen" v-show="!isLoading" :class="{ 'flash' : isShotPhoto }">
                        
                        <div :class="{'flash' : isShotPhoto}"></div>
                        
                        <video v-show="!isPhotoTaken" ref="camera" :width="450" :height="337.5" autoplay></video>
                        
                        <canvas v-show="isPhotoTaken" id="photoTaken" ref="canvas" :width="450" :height="337.5"></canvas>
                    </div>
                    
                    <div v-if="isCameraOpen && !isLoading">
                        <button type="button" class="button" @click="takePhoto">
                        <img src="https://img.icons8.com/material-outlined/50/000000/camera--v2.png">
                        </button>
                    </div>
                    
                    <div v-if="isPhotoTaken && isCameraOpen">
                        <a id="downloadPhoto" download="my-photo.jpg" class="button" role="button" @click="downloadImage">
                        Download
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
export default {
    data() {
        return {
        isCameraOpen: false,
        isPhotoTaken: false,
        isShotPhoto: false,
        isLoading: false,
        link: '#'
        }
    },
    
    methods: {
        toggleCamera() {
            if(this.isCameraOpen) {
                this.isCameraOpen = false;
                this.isPhotoTaken = false;
                this.isShotPhoto = false;
                this.stopCameraStream();
            } else {
                this.isCameraOpen = true;
                this.createCameraElement();
            }
        },
        
        createCameraElement() {
        this.isLoading = true;
        
        const constraints = (window.constraints = {
            audio: false,
            video: true
        });


        navigator.mediaDevices
            .getUserMedia(constraints)
            .then(stream => {
        this.isLoading = false;
            this.$refs.camera.srcObject = stream;
        })
            .catch(error => {
        this.isLoading = false;
            alert("May the browser didn't support or there is some errors.");
        });
        },
        
        stopCameraStream() {
        let tracks = this.$refs.camera.srcObject.getTracks();

                tracks.forEach(track => {
                    track.stop();
                });
        },
        
        takePhoto() {
        if(!this.isPhotoTaken) {
            this.isShotPhoto = true;

            const FLASH_TIMEOUT = 50;

            setTimeout(() => {
            this.isShotPhoto = false;
            }, FLASH_TIMEOUT);
        }
        
        this.isPhotoTaken = !this.isPhotoTaken;
        
        const context = this.$refs.canvas.getContext('2d');
        context.drawImage(this.$refs.camera, 0, 0, 450, 337.5);
        },
        
        downloadImage() {
        const download = document.getElementById("downloadPhoto");
        const canvas = document.getElementById("photoTaken").toDataURL("image/jpeg")
        .replace("image/jpeg", "image/octet-stream");
        download.setAttribute("href", canvas);
        }
    }
};
</script>
<style>
</style>
