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

Although noise may appear to be limited and uninteresting, when it is applied to unlabeled data, it has a compound
benefit of enforcing local smoothness in the decision function on both labeled and unlabeled data. Different kinds of
noise, however, may have different effects. **When data augmentation noise is used, the student must ensure that a translated image, for example, should have the same category
with a non-translated image**. This invariance constraint reduces the degrees of freedom in the model. **When dropout
and stochastic depth are used, the teacher model behaves
like an ensemble of models (when it generates the pseudo
labels, dropout is not used), whereas the student behaves
like a single model**. In other words, the student is forced to
mimic a more powerful ensemble model.

The architectures for the student and teacher models can
be the same or different. However an important requirement
for Noisy Student to work well is that the student model
needs to be sufficiently large to fit more data (labeled and
pseudo labeled). For this purpose, we use the recently developed EfficientNet architectures [69] because they have a
larger capacity than ResNet architectures [23]. Secondly,
to enable the student to learn a more powerful model, we
also make the student model larger than the teacher model.
This is an important difference between our work and prior
works on teacher-student framework whose main goal is
model compression.

We find that Noisy Student is better with an additional
trick: data balancing. Specifically, as all classes in ImageNet have a similar number of labeled images, we also
need to balance the number of unlabeled images for each
class. We duplicate images in classes where there are not
enough images. For classes where we have too many images, we take the images with the highest confidence.
Finally, in the above, we say that the pseudo labels can
be soft or hard. In our experiments, we observe that soft
pseudo labels are usually more stable and lead to faster convergence, especially when the teacher model has low accuracy. Hence we use soft pseudo labels for our experiments
unless otherwise specified.
