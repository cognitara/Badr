# Badr AI Receptionist Testing Framework

This document outlines the systematic testing approach for the Badr AI Receptionist project.

## Testing Philosophy

Our testing approach is based on the following principles:

1. **Comprehensive Coverage**: Test all components and their interactions
2. **Automation**: Automate tests where possible to ensure consistency
3. **Real-world Validation**: Supplement automated tests with real-world testing
4. **Continuous Improvement**: Use test results to drive improvements

## Test Types

### 1. Unit Tests

Tests for individual components in isolation.

- **Face Recognition Tests**: Verify recognition accuracy with different images
- **NLP Tests**: Validate intent detection and response generation
- **Hardware Interface Tests**: Ensure proper interaction with physical components
- **State Machine Tests**: Verify correct state transitions

### 2. Integration Tests

Tests for interactions between components.

- **Face Recognition + Notification**: Verify notifications are sent when faces are recognized
- **Motion Detection + Camera**: Ensure camera activates when motion is detected
- **Speech + NLP**: Validate speech input is correctly processed by NLP
- **NLP + Response Generation**: Verify appropriate responses are generated

### 3. System Tests

End-to-end tests of the entire system.

- **Visitor Scenarios**: Simulate complete visitor interactions
- **Appointment Scheduling**: Test full appointment scheduling workflow
- **Error Handling**: Verify system recovers from various error conditions
- **Long-running Tests**: Ensure stability over extended periods

### 4. Performance Tests

Tests for system performance under various conditions.

- **Load Testing**: Verify system handles multiple interactions
- **Resource Usage**: Monitor CPU, memory, and disk usage
- **Response Time**: Measure time to respond to various inputs
- **Concurrent Operations**: Test multiple operations happening simultaneously

## Test Environment Setup

### VSCode Testing Integration

1. **Install Python Test Explorer Extension**:
   ```bash
   code --install-extension littlefoxteam.vscode-python-test-adapter
   ```

2. **Configure Test Discovery**:
   Create `.vscode/settings.json` with:
   ```json
   {
     "python.testing.pytestEnabled": true,
     "python.testing.unittestEnabled": false,
     "python.testing.nosetestsEnabled": false,
     "python.testing.pytestArgs": [
       "tests"
     ]
   }
   ```

3. **Install Testing Dependencies**:
   ```bash
   pip install pytest pytest-cov pytest-xdist pytest-html
   ```

## Test Directory Structure

```
/tests
  /unit                  # Unit tests
    /face_recognition    # Face recognition tests
    /nlp                 # NLP tests
    /hardware            # Hardware interface tests
    /core                # Core functionality tests
  /integration           # Integration tests
  /system                # System tests
  /performance           # Performance tests
  conftest.py            # Shared test fixtures
  pytest.ini             # Test configuration
```

## Running Tests in VSCode

### Step-by-Step Guide

1. **Open the Testing View**:
   - Click on the flask icon in the activity bar
   - Or use the keyboard shortcut: `Ctrl+Shift+T`

2. **Run All Tests**:
   - Click the play button at the top of the Testing view

3. **Run Specific Tests**:
   - Expand the test tree
   - Click the play button next to a specific test or test file

4. **View Test Results**:
   - Test results appear in the Testing view
   - Failed tests show error messages
   - Click on a test to see detailed output

### Running Tests from Terminal

For more control or when running on the Raspberry Pi without VSCode:

1. **Run All Tests**:
   ```bash
   cd /home/pi/Badr
   python -m pytest
   ```

2. **Run Specific Test Categories**:
   ```bash
   # Run unit tests
   python -m pytest tests/unit

   # Run integration tests
   python -m pytest tests/integration

   # Run system tests
   python -m pytest tests/system
   ```

3. **Generate HTML Report**:
   ```bash
   python -m pytest --html=report.html
   ```

## Test Fixtures

Common test fixtures are defined in `tests/conftest.py`:

- **mock_camera**: Provides a mock camera for testing
- **mock_pir_sensor**: Simulates PIR sensor events
- **mock_audio**: Provides mock audio input/output
- **test_faces**: Sample face images for recognition testing
- **test_audio_samples**: Sample audio files for speech testing

## Writing Tests

### Example Unit Test

```python
# tests/unit/face_recognition/test_face_recognizer.py

def test_face_recognition_accuracy(mock_camera, test_faces):
    """Test face recognition accuracy with known faces."""
    from app.face_recognition.face_recognizer import FaceRecognizer
    
    recognizer = FaceRecognizer()
    
    # Test with different known faces
    for face_name, face_image in test_faces.items():
        result = recognizer.identify_face(face_image)
        assert result == face_name
```

### Example Integration Test

```python
# tests/integration/test_motion_camera.py

def test_motion_triggers_camera(mock_pir_sensor, mock_camera):
    """Test that motion detection triggers the camera."""
    from app.hardware.pir_sensor import PIRSensor
    from app.hardware.camera import Camera
    from app.core.state_machine import StateMachine
    
    state_machine = StateMachine()
    pir_sensor = PIRSensor(state_machine)
    camera = Camera(state_machine)
    
    # Simulate motion detection
    mock_pir_sensor.trigger_motion()
    
    # Verify camera was triggered
    assert mock_camera.capture_called
```

## Continuous Integration

For automated testing on every code change:

1. **Set Up GitHub Actions**:
   Create `.github/workflows/test.yml` with:
   ```yaml
   name: Run Tests
   
   on:
     push:
       branches: [ main ]
     pull_request:
       branches: [ main ]
   
   jobs:
     test:
       runs-on: ubuntu-latest
       steps:
       - uses: actions/checkout@v2
       - name: Set up Python
         uses: actions/setup-python@v2
         with:
           python-version: '3.9'
       - name: Install dependencies
         run: |
           python -m pip install --upgrade pip
           pip install -r requirements.txt
           pip install pytest pytest-cov
       - name: Test with pytest
         run: |
           pytest --cov=app
       - name: Upload coverage report
         uses: codecov/codecov-action@v1
   ```

## Test Monitoring and Reporting

### Real-time Monitoring

1. **Terminal-based Monitoring**:
   ```bash
   pytest-watch -- tests/
   ```

2. **VSCode Live Testing**:
   - Enable auto-run tests in VSCode settings
   - Tests run automatically as you save files

### Test Reports

1. **Coverage Reports**:
   ```bash
   pytest --cov=app --cov-report=html
   ```

2. **HTML Test Reports**:
   ```bash
   pytest --html=report.html
   ```

3. **JUnit XML Reports** (for CI integration):
   ```bash
   pytest --junitxml=results.xml
   ```

## Troubleshooting Tests

### Common Issues

1. **Hardware Access**:
   - Tests requiring hardware access may fail in CI environments
   - Use mocks and dependency injection to isolate hardware dependencies

2. **Timing Issues**:
   - Asynchronous operations may cause flaky tests
   - Use appropriate waits or mock timing-dependent components

3. **Environment Dependencies**:
   - Tests may depend on specific environment variables or configurations
   - Use fixtures to set up and tear down test environments

### Debugging Failed Tests

1. **Verbose Output**:
   ```bash
   pytest -v tests/path/to/failing/test.py
   ```

2. **Print Debugging**:
   ```bash
   pytest -v tests/path/to/failing/test.py --capture=no
   ```

3. **Interactive Debugging**:
   ```bash
   pytest --pdb tests/path/to/failing/test.py
   ```

## Conclusion

This testing framework provides a comprehensive approach to ensuring the quality and reliability of the Badr AI Receptionist system. By following these guidelines, we can maintain high standards of quality while continuing to develop and enhance the system.

---

Powered by Cognitara (c) 2025
