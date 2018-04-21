# Before Deeplearning using PyTorch

## 장비 구성

당연히 예산에 제한이 없으면 가장 비싼 제품들로만 pick하면 될 수 있습니다. 하지만 현실은 다르기에, 여러가지 고려해야 할 점들을 우선순위별로 나열 해 보겠습니다.

### CPU

잘 짜여진 PyTorch 코드는 대부분 GPU 사용량을 최대화 합니다. 따라서 보통의 경우 parallel한 연산은 모두 GPU에 넘어가게 되고, 일부 피할 수 없는 sequential한 연산만 남아 CPU의 사용량은 1개 core에 집중되어 100% 내외를 가리키게 됩니다. 따라서, Core의 숫자가 많은 것도 좋지만, 개별 코어의 clock이 높은 것이 더 중요합니다.

물론 본격적인 딥러닝을 하기 이전에 preprocessing 또는 word embedding의 단계에서는 CPU core가 많은 것이 좋을 수 있습니다. 따라서 이러한 작업간의 중요도를 잘 고려하여 CPU를 선택하면 됩니다. 잘 모르겠고 귀찮을 땐 그냥 _**i7-?700K**_를 하면 됩니다.

결론: core 갯수보단 clock이 높아야 한다.

### RAM

![](/assets/pytorch-intro-ram.png)

메모리 가격이 하늘 높은 줄 모르고 치솟고 있습니다. 이러한 상황에서 원하는 만큼의 메모리를 확보하는 것은 쉬운일이 아닙니다. 하지만 메모리가 최소 16GB에서 권장 32GB는 되어야 합니다. 보통 Xeon CPU가 아닌 메인보드의 경우에는 4개 슬롯에 64GB가 최대치인 경우가 많습니다. 보통 preprocessing 작업을 할 때에 메모리가 많이 필요할 수 있습니다. 따라서 어느정도의 메모리는 시스템 구성에 필요합니다.

결론: 메모리는 많을 수록 좋다. 모르면 32GB

### GPU

![DGX-1](http://images.nvidia.com/content/technologies/deep-learning/images/dgx-1-front.jpg)  
딥러닝 연구자들에게 꿈의 머신, Nvidia DGX-1

일반적인 사용자라면 Nvidia GTX 계열의 Graphic Card를 보통 선택하면 됩니다. \(모든 deep learning framework은 CUDA와 함께 동작하기 때문에 Radeon 그래픽 카드는 소용이 없습니다.\) Cuda Core가 많고, clock이 높을 수록 속도가 빠른것을 의미합니다. memory bandwidth도 매우 중요합니다. 가장 중요한것은 memory size입니다. Memory size가 가장 큰 GPU일수록 고가이기도 합니다. 대략 9세대\(maxwell\)보다 10세대\(pascal\)의 경우 1.3배 정도 속도 차이가 납니다.

메모리가 클 수록 더 큰 배치사이즈를 돌릴 수 있습니다. 또한 크고 복잡한 아키텍쳐를 GPU에 올릴 수 있습니다. 크고 복잡한 아키텍쳐인데 메모리 사이즈가 작으면 작은 배치사이즈로 돌려야 하고, 훈련 속도는 역시 느려지게 될 것 입니다. \(참고: 배치사이즈가 2배 크다고 훈련이 2배 빠르지는 않습니다.\) 또한, 메모리가 넉넉하면 GPU memory에 애초에 모든 데이터를 로드 한 채로 훈련을 실행 시킬 수도 있습니다. 이는 구현의 난이도를 매우 낮추어 줄 것 입니다.

결론: 메모리가 클 수록 좋다. 하지만 메모리가 크면 비싸다.

### Power

파워 서플라이에는 돈을 아끼면 안됩니다. 실제 700W를 뽑아주는 녀석을 장착하면 그래픽 카드 1개 기준으로 부족할 일은 없습니다. \(단, 중급 그래픽 카드의 경우에는 600W도 가능\)

결론: 700W. 뻥파워는 안됩니다.

### Cooling System

GPU에서 뿜어져 나오는 열이 엄청나기 때문에 쿨링 시스템이 매우 중요합니다. 따라서 케이스의 선택도 중요하고, 내부에 fan을 설치하는 것도 좋습니다.
