# bitnet.cpp
[![라이선스: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)
![버전](https://img.shields.io/badge/version-1.0-blue)

[<img src="./assets/header_model_release.png" alt="Hugging Face의 BitNet 모델" width="800"/>](https://huggingface.co/microsoft/BitNet-b1.58-2B-4T)

[데모](https://bitnet-demo.azurewebsites.net/)를 통해 시도해보거나, 자신의 CPU에서 [빌드하고 실행](https://github.com/microsoft/BitNet?tab=readme-ov-file#build-from-source)해보세요.

bitnet.cpp는 1비트 LLM(예: BitNet b1.58)의 공식 추론 프레임워크입니다. 이 프레임워크는 CPU에서 1.58비트 모델의 **빠르고** **무손실** 추론을 지원하는 최적화된 커널 세트를 제공합니다(NPU와 GPU 지원은 다음에 추가될 예정).

bitnet.cpp의 첫 번째 릴리스는 CPU에서의 추론을 지원합니다. bitnet.cpp는 ARM CPU에서 **1.37배**에서 **5.07배**까지의 속도 향상을 달성했으며, 더 큰 모델일수록 더 큰 성능 향상을 경험합니다. 또한 에너지 소비를 **55.4%**에서 **70.0%**까지 줄여 전반적인 효율성을 더욱 향상시켰습니다. x86 CPU에서는 **2.37배**에서 **6.17배**까지의 속도 향상과 **71.9%**에서 **82.2%** 사이의 에너지 감소를 보여줍니다. 또한 bitnet.cpp는 단일 CPU에서 100B BitNet b1.58 모델을 실행할 수 있으며, 인간의 읽기 속도(초당 5-7 토큰)에 필적하는 속도를 달성하여 로컬 장치에서 LLM을 실행할 수 있는 잠재력을 크게 향상시켰습니다. 자세한 내용은 [기술 보고서](https://arxiv.org/abs/2410.16144)를 참조하세요.

<img src="./assets/m2_performance.jpg" alt="m2_performance" width="800"/>
<img src="./assets/intel_performance.jpg" alt="m2_performance" width="800"/>

>테스트된 모델은 bitnet.cpp의 추론 성능을 입증하기 위한 연구 맥락에서 사용된 더미 설정입니다.

## 데모

Apple M2에서 BitNet b1.58 3B 모델을 실행하는 bitnet.cpp의 데모:

https://github.com/user-attachments/assets/7f46b736-edec-4828-b809-4be780a3e5b1

## 최신 소식:
- 04/14/2025 [Hugging Face의 BitNet 공식 2B 파라미터 모델](https://huggingface.co/microsoft/BitNet-b1.58-2B-4T) ![NEW](https://img.shields.io/badge/NEW-red)
- 02/18/2025 [Bitnet.cpp: 3진 LLM을 위한 효율적인 엣지 추론](https://arxiv.org/abs/2502.11880)
- 11/08/2024 [BitNet a4.8: 1비트 LLM을 위한 4비트 활성화](https://arxiv.org/abs/2411.04965)
- 10/21/2024 [1비트 AI 인프라: Part 1.1, CPU에서의 빠르고 무손실 BitNet b1.58 추론](https://arxiv.org/abs/2410.16144)
- 10/17/2024 bitnet.cpp 1.0 릴리스
- 03/21/2024 [The-Era-of-1-bit-LLMs__Training_Tips_Code_FAQ](https://github.com/microsoft/unilm/blob/master/bitnet/The-Era-of-1-bit-LLMs__Training_Tips_Code_FAQ.pdf)
- 02/27/2024 [1비트 LLM의 시대: 모든 대형 언어 모델은 1.58비트입니다](https://arxiv.org/abs/2402.17764)
- 10/17/2023 [BitNet: 대형 언어 모델을 위한 1비트 트랜스포머 확장](https://arxiv.org/abs/2310.11453)

## 감사의 말

이 프로젝트는 [llama.cpp](https://github.com/ggerganov/llama.cpp) 프레임워크를 기반으로 합니다. 오픈소스 커뮤니티에 기여한 모든 저자들에게 감사드립니다. 또한 bitnet.cpp의 커널은 [T-MAC](https://github.com/microsoft/T-MAC/)에서 선구적으로 개발된 Lookup Table 방법론을 기반으로 구축되었습니다. 3진 모델을 넘어서는 일반적인 저비트 LLM의 추론을 위해서는 T-MAC를 사용하는 것을 권장합니다.
## 공식 모델
<table>
    </tr>
    <tr>
        <th rowspan="2">모델</th>
        <th rowspan="2">파라미터</th>
        <th rowspan="2">CPU</th>
        <th colspan="3">커널</th>
    </tr>
    <tr>
        <th>I2_S</th>
        <th>TL1</th>
        <th>TL2</th>
    </tr>
    <tr>
        <td rowspan="2"><a href="https://huggingface.co/microsoft/BitNet-b1.58-2B-4T">BitNet-b1.58-2B-4T</a></td>
        <td rowspan="2">2.4B</td>
        <td>x86</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
        <td>&#9989;</td>
    </tr>
    <tr>
        <td>ARM</td>
        <td>&#9989;</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
    </tr>
</table>

## 지원 모델
❗️**bitnet.cpp의 추론 기능을 입증하기 위해 [Hugging Face](https://huggingface.co/)에서 사용 가능한 기존 1비트 LLM을 사용합니다. bitnet.cpp의 릴리스가 모델 크기와 학습 토큰 측면에서 대규모 설정에서 1비트 LLM의 개발에 영감을 줄 수 있기를 바랍니다.**

<table>
    </tr>
    <tr>
        <th rowspan="2">모델</th>
        <th rowspan="2">파라미터</th>
        <th rowspan="2">CPU</th>
        <th colspan="3">커널</th>
    </tr>
    <tr>
        <th>I2_S</th>
        <th>TL1</th>
        <th>TL2</th>
    </tr>
    <tr>
        <td rowspan="2"><a href="https://huggingface.co/1bitLLM/bitnet_b1_58-large">bitnet_b1_58-large</a></td>
        <td rowspan="2">0.7B</td>
        <td>x86</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
        <td>&#9989;</td>
    </tr>
    <tr>
        <td>ARM</td>
        <td>&#9989;</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
    </tr>
    <tr>
        <td rowspan="2"><a href="https://huggingface.co/1bitLLM/bitnet_b1_58-3B">bitnet_b1_58-3B</a></td>
        <td rowspan="2">3.3B</td>
        <td>x86</td>
        <td>&#10060;</td>
        <td>&#10060;</td>
        <td>&#9989;</td>
    </tr>
    <tr>
        <td>ARM</td>
        <td>&#10060;</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
    </tr>
    <tr>
        <td rowspan="2"><a href="https://huggingface.co/HF1BitLLM/Llama3-8B-1.58-100B-tokens">Llama3-8B-1.58-100B-tokens</a></td>
        <td rowspan="2">8.0B</td>
        <td>x86</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
        <td>&#9989;</td>
    </tr>
    <tr>
        <td>ARM</td>
        <td>&#9989;</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
    </tr>
    <tr>
        <td rowspan="2"><a href="https://huggingface.co/collections/tiiuae/falcon3-67605ae03578be86e4e87026">Falcon3 패밀리</a></td>
        <td rowspan="2">1B-10B</td>
        <td>x86</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
        <td>&#9989;</td>
    </tr>
    <tr>
        <td>ARM</td>
        <td>&#9989;</td>
        <td>&#9989;</td>
        <td>&#10060;</td>
    </tr>
</table>



## 설치

### 요구사항
- python>=3.9
- cmake>=3.22
- clang>=18
    - Windows 사용자의 경우 [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/)를 설치하세요. 설치 프로그램에서 다음 옵션을 최소한 활성화하세요(이렇게 하면 CMake와 같은 필요한 추가 도구도 자동으로 설치됩니다):
        -  C++를 사용한 데스크톱 개발
        -  Windows용 C++ CMake 도구
        -  Windows용 Git
        -  Windows용 C++ Clang 컴파일러
        -  LLVM-Toolset(clang)에 대한 MS-Build 지원
    - Debian/Ubuntu 사용자의 경우 [자동 설치 스크립트](https://apt.llvm.org/)를 사용하여 다운로드할 수 있습니다:

        `bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"`
- conda (권장)

### 소스에서 빌드

> [!중요]
> Windows를 사용하는 경우, 다음 명령어를 실행할 때 항상 VS2022용 개발자 명령 프롬프트 / PowerShell을 사용하세요. 문제가 발생하면 아래 FAQ를 참조하세요.

1. 저장소 복제
```bash
git clone --recursive https://github.com/microsoft/BitNet.git
cd BitNet
```
2. 의존성 설치
```bash
# (권장) 새로운 conda 환경 생성
conda create -n bitnet-cpp python=3.9
conda activate bitnet-cpp

pip install -r requirements.txt
```
3. 프로젝트 빌드
```bash
# 모델을 수동으로 다운로드하고 로컬 경로로 실행
huggingface-cli download microsoft/BitNet-b1.58-2B-4T-gguf --local-dir models/BitNet-b1.58-2B-4T
python setup_env.py -md models/BitNet-b1.58-2B-4T -q i2_s
```

<pre>
사용법: setup_env.py [-h] [--hf-repo {1bitLLM/bitnet_b1_58-large,1bitLLM/bitnet_b1_58-3B,HF1BitLLM/Llama3-8B-1.58-100B-tokens,tiiuae/Falcon3-1B-Instruct-1.58bit,tiiuae/Falcon3-3B-Instruct-1.58bit,tiiuae/Falcon3-7B-Instruct-1.58bit,tiiuae/Falcon3-10B-Instruct-1.58bit}] [--model-dir MODEL_DIR] [--log-dir LOG_DIR] [--quant-type {i2_s,tl1}] [--quant-embd]
                    [--use-pretuned]

추론 실행을 위한 환경 설정

선택적 인수:
  -h, --help            도움말 메시지 표시
  --hf-repo {1bitLLM/bitnet_b1_58-large,1bitLLM/bitnet_b1_58-3B,HF1BitLLM/Llama3-8B-1.58-100B-tokens,tiiuae/Falcon3-1B-Instruct-1.58bit,tiiuae/Falcon3-3B-Instruct-1.58bit,tiiuae/Falcon3-7B-Instruct-1.58bit,tiiuae/Falcon3-10B-Instruct-1.58bit}, -hr {1bitLLM/bitnet_b1_58-large,1bitLLM/bitnet_b1_58-3B,HF1BitLLM/Llama3-8B-1.58-100B-tokens,tiiuae/Falcon3-1B-Instruct-1.58bit,tiiuae/Falcon3-3B-Instruct-1.58bit,tiiuae/Falcon3-7B-Instruct-1.58bit,tiiuae/Falcon3-10B-Instruct-1.58bit}
                        추론에 사용할 모델
  --model-dir MODEL_DIR, -md MODEL_DIR
                        모델을 저장/로드할 디렉토리
  --log-dir LOG_DIR, -ld LOG_DIR
                        로깅 정보를 저장할 디렉토리
  --quant-type {i2_s,tl1}, -q {i2_s,tl1}
                        양자화 유형
  --quant-embd          임베딩을 f16으로 양자화
  --use-pretuned, -p    사전 조정된 커널 파라미터 사용
</pre>

## 사용법
### 기본 사용법
```bash
# 양자화된 모델로 추론 실행
python run_inference.py -m models/BitNet-b1.58-2B-4T/ggml-model-i2_s.gguf -p "당신은 도움이 되는 어시스턴트입니다" -cnv
```

<pre>
사용법: run_inference.py [-h] [-m MODEL] [-n N_PREDICT] -p PROMPT [-t THREADS] [-c CTX_SIZE] [-temp TEMPERATURE] [-cnv]

추론 실행

선택적 인수:
  -h, --help            도움말 메시지 표시
  -m MODEL, --model MODEL
                        모델 파일 경로
  -n N_PREDICT, --n-predict N_PREDICT
                        텍스트 생성 시 예측할 토큰 수
  -p PROMPT, --prompt PROMPT
                        텍스트를 생성할 프롬프트
  -t THREADS, --threads THREADS
                        사용할 스레드 수
  -c CTX_SIZE, --ctx-size CTX_SIZE
                        프롬프트 컨텍스트 크기
  -temp TEMPERATURE, --temperature TEMPERATURE
                        생성된 텍스트의 무작위성을 제어하는 하이퍼파라미터인 온도
  -cnv, --conversation  채팅 모드를 활성화할지 여부(지시 모델용)
                        (이 옵션이 켜져 있으면 -p로 지정된 프롬프트가 시스템 프롬프트로 사용됩니다.)
</pre>

### 벤치마크
모델을 제공하여 추론 벤치마크를 실행하는 스크립트를 제공합니다.

```  
사용법: e2e_benchmark.py -m MODEL [-n N_TOKEN] [-p N_PROMPT] [-t THREADS]  
   
추론 실행을 위한 환경 설정  
   
필수 인수:  
  -m MODEL, --model MODEL  
                        모델 파일 경로
   
선택적 인수:  
  -h, --help  
                        도움말 메시지 표시
  -n N_TOKEN, --n-token N_TOKEN  
                        생성할 토큰 수
  -p N_PROMPT, --n-prompt N_PROMPT  
                        텍스트 생성에 사용할 프롬프트 토큰 수
  -t THREADS, --threads THREADS  
                        추론 실행에 사용할 스레드 수
```  
   
각 인수에 대한 간략한 설명:  
   
- `-m`, `--model`: 모델 파일 경로. 이는 스크립트를 실행할 때 반드시 제공해야 하는 필수 인수입니다.  
- `-n`, `--n-token`: 추론 중 생성할 토큰 수. 기본값이 128인 선택적 인수입니다.  
- `-p`, `--n-prompt`: 텍스트 생성에 사용할 프롬프트 토큰 수. 기본값이 512인 선택적 인수입니다.  
- `-t`, `--threads`: 추론 실행에 사용할 스레드 수. 기본값이 2인 선택적 인수입니다.  
- `-h`, `--help`: 도움말 메시지를 표시하고 종료합니다. 사용법 정보를 표시하려면 이 인수를 사용하세요.  
   
예시:  
   
```sh  
python utils/e2e_benchmark.py -m /path/to/model -n 200 -p 256 -t 4  
```  
   
이 명령은 `/path/to/model`에 위치한 모델을 사용하여 256 토큰 프롬프트에서 200 토큰을 생성하고, 4개의 스레드를 활용하여 추론 벤치마크를 실행합니다.  

공개 모델에서 지원하지 않는 모델 레이아웃의 경우, 주어진 모델 레이아웃으로 더미 모델을 생성하고 기계에서 벤치마크를 실행하는 스크립트를 제공합니다:

```bash
python utils/generate-dummy-bitnet-model.py models/bitnet_b1_58-large --outfile models/dummy-bitnet-125m.tl1.gguf --outtype tl1 --model-size 125M

# 생성된 모델로 벤치마크 실행, -m으로 모델 경로 지정, -p로 처리할 프롬프트 지정, -n으로 생성할 토큰 수 지정
python utils/e2e_benchmark.py -m models/dummy-bitnet-125m.tl1.gguf -p 512 -n 128
```
### 자주 묻는 질문 (FAQ) 📌 

#### Q1: log.cpp에서 std::chrono 문제로 인해 llama.cpp 빌드가 실패하는 경우?

**A:**
이는 llama.cpp의 최근 버전에서 발생한 문제입니다. 이 [토론](https://github.com/abetlen/llama-cpp-python/issues/1942)에서 이 [커밋](https://github.com/tinglou/llama.cpp/commit/4e3db1e3d78cc1bcd22bcb3af54bd2a4628dd323)을 참조하여 이 문제를 해결하세요.

#### Q2: Windows의 conda 환경에서 clang으로 빌드하는 방법?

**A:** 
프로젝트를 빌드하기 전에 다음 명령을 실행하여 clang 설치와 Visual Studio 도구 접근성을 확인하세요:
```
clang -v
```

이 명령은 올바른 버전의 clang을 사용하고 있고 Visual Studio 도구를 사용할 수 있는지 확인합니다. 다음과 같은 오류 메시지가 표시되면:
```
'clang'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다.
```

이는 명령줄 창이 Visual Studio 도구에 대해 제대로 초기화되지 않았음을 나타냅니다.

• 명령 프롬프트를 사용하는 경우 다음을 실행하세요:
```
"C:\Program Files\Microsoft Visual Studio\2022\Professional\Common7\Tools\VsDevCmd.bat" -startdir=none -arch=x64 -host_arch=x64
```

• Windows PowerShell을 사용하는 경우 다음 명령을 실행하세요:
```
Import-Module "C:\Program Files\Microsoft Visual Studio\2022\Professional\Common7\Tools\Microsoft.VisualStudio.DevShell.dll" Enter-VsDevShell 3f0e31ad -SkipAutomaticLocation -DevCmdArguments "-arch=x64 -host_arch=x64"
```

이 단계들은 환경을 초기화하고 올바른 Visual Studio 도구를 사용할 수 있게 해줍니다.
