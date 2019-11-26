# Self-training with Noisy Student improves ImageNet classification
Algorithm 1 gives an overview of self-training with
Noisy Student (or Noisy Student in short). The inputs to
the algorithm are both labeled and unlabeled images. We
use the labeled images to train a teacher model using the
standard cross entropy loss. We then use the teacher model
to generate pseudo labels on unlabeled images. The pseudo
labels can be soft (a continuous distribution) or hard (a onehot distribution). We then train a student model which minimizes the combined cross entropy loss on both labeled images and unlabeled images. Finally, we iterate the process
by putting back the student as a teacher to generate new
pseudo labels and train a new student.

The algorithm is basically self-training, a method in
semi-supervised learning (e.g., [59, 79]). We will discuss
how our method is related to prior works in Section 5. Our
main change is to add more sources of noise to the student
to significantly improve it while removing the noise in the
teacher when the teacher generates the pseudo labels.
When the student model is deliberately noised it is actually trained to be consistent to the more powerful teacher
model that is not noised when it generates pseudo labels. In
our experiments, we use dropout [63], stochastic depth [29],
data augmentation [14] to noise the student.
